# Meeting Minutes: SVSM Development Call (August 19th, 2026)

## Topics:

### TSC Meeting Update

* **Guest User-Pointer Rework Merged:** Carlos's guest user-pointer rework has been merged.
* **Updated Contribution Guidelines Merged:** The refreshed contribution guidelines are now part of the repository. They primarily document the project's existing practices, including the requirement that commit series remain bisectable.
* **Observability Specification Review Started:** Jörg updated the SVSM specification for the observability and configuration protocol. Internal review is under way before the update can become part of the official specification.
* **GSoC Projects Praised:** The TSC is very happy with the Google Summer of Code results and thanked Nicola and Tanish for their work. The resulting code still needs to be merged, with the observability and configuration protocol work dependent on acceptance of the specification.
* **TPM Persistence Integration Nearing Completion:** PR 1195 connects the TPM to persistence and would bring the project close to supporting TPM-backed disk unlocking in SVSM.
* **TPM PR Should Not Be Rushed for the Release:** The group discussed including PR 1195 in the upcoming release but agreed that correctness is more important and the work can move to the following release if it is not ready.
* **PCID Work Needs Final Review:** The PCID work still needs Jörg's review of the bitmap allocator and its atomic operations, plus Jon's review of the general PCID usage. The TSC expects it can be merged soon.
* **Unresponsive PR Closed:** PR 1091 was closed after its contributor did not explain why the proposed change was needed.
* **KVM Entry Failure Issue Remains Open:** Issue 1081 will remain open until the upstream fix, which has reached stable kernels, is verified in the Azure kernel used by the GitHub runners.
* **EDK2 Fork May Be Archived:** The group will check what remains before archiving its EDK2 fork. The project now relies on upstream projects for guest-side EDK2 and Linux changes and does not plan to maintain downstream guest-side forks.
* **TDX Partitioning Discussion Planned:** The TSC plans an initial discussion about how to move issue 815 forward, followed by a broader discussion when more members are available, likely the week after next.

### Page-Table Redesign

* **Separate Page-Table Crate Deferred:** Jörg told Ziqiao that PRs 1122 through 1124 should not proceed because SVSM's page-table code is about to undergo substantial redesign.
* **Existing Work Can Be Reused Elsewhere:** Ziqiao may copy the proposed crate into LiteBox or other projects. Ziqiao already has a private copy and is pursuing more extensive changes there.
* **Fine-Grained Locking Prototype Discussed:** Ziqiao described a two-level locking design that allows inexpensive read-locked page-table walks and takes stronger locks only for updates. The private implementation has been tested with COCONUT and LiteBox and includes concurrency verification.
* **Prototype Will Be Shared:** Ziqiao plans to share the cleaned-up implementation so the SVSM developers can consider its locking ideas during later optimization work.
* **Global Lock Preferred Initially:** SVSM will likely retain a global page-table lock during the initial redesign and leave finer-grained locking as a later optimization.
* **Current Shared-Path Locking Is Unsound:** Locks currently belong to individual page tables even though page-table parts can be shared by multiple page tables. This does not appear exploitable under current usage, but it must be corrected as SVSM user space becomes more complex.
* **Direct-Map Dependency Will Be Removed:** The current walker depends heavily on the direct map. The redesign will instead make greater use of the existing self-map, which only provides access to the currently active page table.
* **Self-Map Requires a New API:** Page-table modification methods cannot remain simple methods on an arbitrary page-table object when they operate through the active table's self-map. The API must encode this restriction and prevent races.
* **Inactive-Table Updates Are Rare:** The principal case requiring modification of an inactive page table is task creation, when the new task's stack must be mapped before it can run. The group expects this special case can be handled directly.

### Attestation and TPM Persistence

* **Missing Devices Should Not Cause a Panic:** The group agreed that an SVSM image built with attestation and persistence support should continue booting when the device tree does not provide the required attestation-proxy or persistence devices.
* **One Image Should Support Multiple Use Cases:** The fallback allows the same SVSM image to serve both persistent-TPM and ephemeral-TPM deployments. Confidential-container users, for example, are primarily interested in ephemeral TPMs and later runtime attestation rather than persistent TPM secrets.
* **Fallback Produces an Ephemeral TPM:** When the required services are absent, attestation and persistence setup should opt out and the TPM should start with newly manufactured ephemeral state.
* **Host Control Does Not Add Trust:** Although the host controls the device tree, panicking would not provide additional security because a malicious host could also substitute the surrounding attestation and persistence services.
* **Guests Can Detect the Fallback:** A guest expecting persistent state will discover that the TPM identity has changed and will be unable to recover persistent secrets such as a disk-unlocking key.
* **TPM Trust Must Be Re-established on Every Boot:** The TPM is not itself the ultimate root of trust. Before providing secrets, a relying party must validate its identity through its endorsement key and an attestation report tying the TPM to the VM and SVSM instance.
* **Offline Manufacturing Is the Initial Trusted Workflow:** The simplest supported model is for users to manufacture persistent TPM state in a trusted environment, retain the expected TPM identity, and verify it after deployment.
* **Current In-SVSM Manufacturing Needs a Warning:** Until tooling exists for offline manufacturing, the current ability to manufacture persistent state inside SVSM may remain, but documentation must state that this workflow requires trusting the host during manufacturing and is otherwise vulnerable to substitution.
* **Future Online Manufacturing Needs External Endorsement:** Supporting trustworthy first-boot manufacturing in public clouds will require a service such as Trustee to bind or sign the new TPM endorsement key using evidence that it was created inside a genuine attested SVSM instance.
* **Deployment Assumptions Need Documentation:** The group agreed that supported persistence, manufacturing, attestation, and secret-delivery workflows should be documented more thoroughly, potentially in a follow-up PR with a flow diagram.
* **Luigi Will Implement the Non-Panic Fallback:** Luigi volunteered to open a PR that skips unavailable attestation and persistence services instead of panicking.
