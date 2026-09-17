# Meeting Minutes: SVSM Development Call (September 9th, 2026)

## Topics:

### TSC Meeting Update

* **Large PRs Need Meaningful Cover Letters:** Contributors submitting large changes should explain why the change is needed, describe relevant architectural details, and provide enough context for reviewers to assess the series.
* **Contribution Guidance Will Be Updated:** Carlos has a pending update to the contribution guide documenting the cover-letter expectation.
* **PR Descriptions Will Feed Merge Messages:** A GitHub setting was enabled to include the PR description in the merge commit message. Maintainers can still edit the message when merging, but a good PR description should minimize the work required.
* **Secure Timer Requirements Remain Under Discussion:** The TSC discussed the secure monitoring timer API and whether its timing source must itself be secure. The group identified a way forward but did not reach a final conclusion.
* **Rebased Linux and QEMU Branches Need Testing:** The planes patch set has been rebased onto Linux 7.2, with additional support for the in-kernel I/O APIC and device assignment. Related QEMU changes are also available, and community testing is requested.
* **Both Host Components Must Be Updated Together:** The rebased Linux and QEMU branches include userspace API changes and must be tested as a matching pair.
* **Rebased Branches May Become the Defaults Soon:** One reported problem has already been fixed. If testing finds no major issues, Jörg plans to make the rebased branches the defaults near the beginning of the following week.

### Shared Crypto Implementation for Cocoon TPM and CocoonFS

* **Current CocoonFS Work Duplicates OpenSSL:** Oliver's work-in-progress integration currently builds a second OpenSSL instance, copied from the Cocoon TPM setup with the same configuration.
* **One Shared OpenSSL Build Is the Immediate Goal:** The group agreed that the CocoonFS PR must not merge with two copies of OpenSSL. Attestation, the TPM, and CocoonFS should share one crypto implementation at the PR boundary, even if individual commits temporarily need a different arrangement for bisectability.
* **A Rust `-sys` Crate Can Provide the Shared Build:** Nicolai proposed wrapping the C library in a conventional Rust system crate and using Cargo's [`links` manifest key](https://doc.rust-lang.org/cargo/reference/build-scripts.html#the-links-manifest-key) to communicate the library and header locations to dependent build scripts. This should let both Cocoon TPM and CocoonFS link the same static OpenSSL build without introducing a CocoonFS dependency on the TPM.
* **Oliver and Nicolai Will Coordinate:** Oliver will investigate the shared-linking approach with Nicolai and revise the work-in-progress PR.
* **Crypto Must Remain Replaceable:** The longer-term design should retain a clear abstraction boundary so deployments can select OpenSSL, BoringSSL, or RustCrypto according to their requirements. The Cocoon TPM crypto crate is intended to provide that selection point.
* **CocoonFS Uses Crypto Primitives Rather Than TLS:** CocoonFS needs symmetric encryption, hashing, and elliptic-curve primitives for its encrypted persistent-storage format, rather than transport encryption. The existing reduced OpenSSL configuration may therefore remain sufficient.
* **Storage Is Authenticated but Whole-Image Rollback Remains Possible:** The filesystem format authenticates encrypted data using a key obtained from the KBS. An attacker can currently revert the entire image to an earlier snapshot; preventing that requires an external trusted mechanism. The group suggested security review of the design.
* **Design References Shared:** Nicolai shared the [Cocoon TPM crypto overview](https://github.com/coconut-svsm/cocoon-tpm/blob/main/crypto/README.md) and the [CocoonFS on-disk format](https://coconut-svsm.github.io/cocoon-tpm/cocoonfs/cocoonfs-format.html).
* **Kernel/User-Space Crypto Placement Is Future Work:** Moving TPM and attestation functions to user space may require shared or separately instantiated crypto modules. The group deferred that design and will begin with a single crypto implementation for all current consumers.

### Conference BoF Discussion

* **Little Interest Shown for an LPC BoF:** The call did not identify enough immediate interest to organize an SVSM BoF at Linux Plumbers Conference. Anyone who would still like one should contact Jörg.
* **KVM Forum May Be a Better Fit:** Several community members expect to attend KVM Forum, whose program has a stronger concentration of Coconut-related topics. The group will revisit interest shortly before the event.
* **KVM Forum BoFs Can Be Organized On Site:** Stefano said BoFs are normally proposed on a whiteboard during the first day and held later that day, so no immediate advance booking is needed.
* **Remote Participation Is a Trade-Off:** LPC has remote-participation infrastructure, while KVM Forum is expected to be in-person only.

### ELF Loader RELRO Support

* **Mahmoud Plans to Work on RELRO:** Mahmoud confirmed that nobody else is currently implementing the [RELRO support tracked in issue #448](https://github.com/coconut-svsm/svsm/issues/448) and volunteered to take it on.
* **Enforcement Point Needs Design Work:** Current user-space binaries are built without PIE, but the implementation should account for possible future position-independent binaries. Mahmoud is leaning toward applying read-only relocation protection after mapping and relocation but before execution.
* **Mapping APIs Will Need Protection Flags:** The work is expected to touch virtual-memory mapping because the current range and page mapping interfaces do not carry the required protection flags.
* **An RFC or PR Will Start the Detailed Review:** Mahmoud plans to post a focused initial implementation soon. The group will use the code to discuss the design and generalize it later if additional use cases emerge.

### Administrative Reminder

* **LPC Microconference Schedule Needs Submission:** James reminded Jörg to enter the already-prepared LPC microconference schedule into the conference system.
