# Meeting Minutes: SVSM Development Call (April 1st, 2026)

## Topics:

### TSC Meeting Update

* **Personnel Announcement:** Jörg Rödel will be on PTO starting Friday and through next week; Stefano Garzarella will chair the next meeting.
* **User Mode Testing PR:** The TSC wants to move forward with the user mode testing PR (#926) as it is a dependency for upcoming work.
    * **Feedback:** The TSC requested using a separate binary (e.g., `test-init`) rather than the standard `init` for testing.
* **March Release Recap:** The release was finalized last Friday.
    * **Security:** The OpenSSF scorecard rating improved from 7.9 to 8.8.
    * **CI Fixes:** Issues regarding the verification workflow, specifically downloading and executing binaries, have been resolved.
* **Feature Detectability:** Brief discussion regarding VSOCK PR and feature detectability; this topic will be continued in future meetings.

### Technical Discussions & PR Updates

* **Library & CI Issues (PR 926):** Carlos López confirmed that CI issues related to the  PR #998 (xbuild: use packit as a library) are fixed.
    * The issue involved incorrect linking of the C runtime (libc) when running tests on single packages versus the whole workspace, leading to symbol conflicts and segfaults.
    * The solution involved not linking the custom C runtime and its defined symbols (malloc, free, etc.).
* **Guest Pointer Issue (#659):** Carlos is working on a PR to address guest pointer semantics.
    * The goal is to create a new API that serves as a safe memory accessor without "guest" in the name, as the current `GuestPtr` is used for non-guest memory.
    * Future work includes supporting dynamically sized types (slices).
* **Copy-on-Write (CoW) Logic:** Carlos questioned the removal of CoW logic from file mappings.
    * Jörg clarified that CoW is implemented in `PageRef` and utilized by the ELF loader for data sections.
    * Kernel `mmap` does support private mappings, but PR is not merged yet.

### Project Updates

* **Cocoon TPM & Storage:** Oliver Steffen is reviewing the Cocoon TPM codebase to support future storage implementation.
    * He is currently writing unit tests and exploring OpenSSL as an alternative to the BoringSSL backend.

### Upcoming Business

* **IGVM Measurement/CoRIM Discussion:** Representatives from the IGVM project will attend next week's meeting to discuss measurements and CoRIM.
* **Next Meeting:** Will be chaired by Stefano Garzarella.
