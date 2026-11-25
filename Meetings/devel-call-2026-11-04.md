# Meeting Minutes: SVSM Development Call (November 4th, 2026)

## Topics:

### TSC Meeting Update and Review Process

* **Review Throughput Is Limiting AI Productivity Gains:** The TSC discussed how to adapt review and merge processes to the increased volume of changes enabled by AI. Jörg said responsible use of AI for contributions is welcome, but the project cannot fully benefit while reviews lag behind. The discussion remains open to the wider community.
* **AI-Assisted Review Should Leave More Time for Architecture:** The proposed direction is to use AI more extensively for correctness and regression checks, while human reviewers focus on scope, architecture, and project direction. Automated PR review would require both a bot and donated AI capacity; reviewers currently use the tools available to them manually.
* **A One-Week Feedback Target Is Under Discussion:** The TSC considered a target for every PR to receive feedback within a week. No final decision has been made.
* **PR State Labels Would Clarify Who Needs to Act:** Proposed states would distinguish PRs blocked by dependencies, waiting for the submitter, and waiting for review. The workflow would be documented so contributors can update labels after addressing feedback. Label changes require triage permissions, which regular contributors may have but new contributors generally do not. Mahmoud confirmed that he had been unable to remove a rebase label himself. Stefano will investigate a bot to help manage this workflow without granting everyone triage access.
* **Direct-Map Dependency Removal Needs Further Review:** Jörg's review identified inefficiencies related to VMR page-table parts and use of VMRs for the per-CPU area. Removing page-table parts would also require ensuring that VMR operations only affect mappings in the active page table, potentially through interface changes. Carlos reported an updated approach that checks whether a page-table part belongs to the active table by comparing physical addresses at the known PML4 index. He believes this allows the optimizations without intrusive VMR changes. One issue remains in the updated PR, and Jörg will review it.
* **PCID Handling Update Is Awaiting Review:** The TSC identified problems involving page-table root allocation and TLB translations for the self-map. Jörg communicated the issues to Tanish, who submitted an update that Jörg has not yet reviewed.

### Linux-Compatible Syscalls and Musl User Space

* **Conversion Can Be Staged Without Preserving the Existing API:** Mahmoud proposed converting the syscalls already close to Linux semantics first, temporarily assigning SVSM-specific numbers outside the Linux range to the remaining calls. Jörg initially preferred converting existing calls together, with one commit per syscall, since there is no stable API to preserve. After discussing the larger directory-handling changes and the smaller set needed for Hello World, he agreed that staging the conversion makes sense.
* **New Syscalls Should Be Separate from Conversion Work:** Existing syscall conversions can be grouped in one PR, while new functionality needed for the musl-linked Hello World program should be submitted separately. Mahmoud identified `set_tid_address` and `arch_prctl` support for the FS base, including per-task state, among the additions needed for that prototype.
* **File Descriptors Need Linux Numbering and Per-Task State:** The initial descriptors should use the conventional numbers 0, 1, and 2; the current output descriptor uses 0. Mahmoud also plans to make descriptor state per-task so one task's changes do not affect others. This work will follow his currently open error-number compatibility PR.
* **The Initial User-Space Stack Will Be Updated:** Jörg noted that musl expects an initial stack containing arguments, environment information, and related loader data. Mahmoud has changes for the execution path and plans to include them in the follow-up Hello World PR.

### Systemd Integration and Fedora Packaging

* **A Working Integration Branch Exists:** Paul Meyer has added COCONUT guest support to `systemd-vmspawn` and made corresponding changes to systemd PID 1. He also has COCONUT support working in the configfs TSM signer for systemd's reporting infrastructure, which collects system information and metrics.
* **Fedora Packaging Is Waiting for Review:** Luigi said his packaging work is seeking reviews, and Paul offered to help move it forward. Paul questioned whether the SNP-specific firmware descriptor used there provides the TPM driver or whether the generic one is needed. Luigi expected TPM support to be enabled by default and will check; the question was not resolved during the call.

### TPM Attestation and Signing Keys

* **Paul Wants to Avoid an Interactive Credential Exchange:** The current attestation report includes the endorsement key's public structure. Binding that to an attestation key requires the TCG MakeCredential/ActivateCredential flow, which Paul would like to avoid for ephemeral confidential-computing workloads. He asked whether the attestation key could instead be included directly in the report.
* **A Template-Based SVSM Extension Could Provide a Signing EK:** James described Dionna's earlier proposal to let callers supply a key template to the attestation service, which would create and certify the key. A signing endorsement key could then serve the role of an attestation key. This would be an SVSM specification extension; the current interface does not accept such a template. No implementation decision was made.
* **The Recent TPM Command Proposal Addresses Related Needs:** Nicolai pointed to the recent mailing-list proposal for a new TPM command. James said that establishing the binding through TCG would take longer, while an SVSM specification change is under the project's control. Paul requested pointers to both discussions.
* **Older Mailing-List Archives Need to Be Recovered:** James found part of the earlier discussion under the subject "vTPM service attestation format update" and shared a link in chat, but the beginning of the thread was missing from the available archive. Jörg will look for the archives from his former mailing-list server and see how to make them shareable.

### Shared Crypto Backend

* **Luigi Is Moving RustCrypto Use Behind Cocoon TPM's Crypto Layer:** Before the formal start of the call, Luigi asked Nicolai to review his crypto PR. Nicolai expects to look at it next week. Additional Cocoon TPM work will be needed, including AES-GCM support across the three backends; Nicolai offered to implement missing functionality if Luigi opens issues.
* **Missing Higher-Level Operations Can Be Written in Rust:** Luigi noted that a derivation operation needed for attestation is unavailable in BoringSSL. Nicolai was comfortable implementing higher-level modes or operations in Rust over the backend's existing cryptographic primitives.
