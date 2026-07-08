# Meeting Minutes: SVSM Development Call (July 8th, 2026)

## Topics:

### TSC Meeting Update

* **Rust Toolchain Update Planned:** Jörg said the TSC discussed raising the minimum supported Rust version from 1.88, initially to 1.92 and subsequently considering 1.94. An update is expected after the remaining issues are resolved.
* **Toolchain Update Policy Needed:** Because minimum-version changes affect downstream consumers packaging SVSM, the project plans to document when and why the toolchain is updated. The policy should make the process transparent and give downstream users an opportunity to provide feedback.
* **Fallible Allocation Work Progressing:** Carlos reported continued progress on fallible allocation support. Some questions remain open, but the work is moving forward.
* **User-Space and LiteBox Strategy Remains Open:** The TSC discussed whether SVSM should rely fully on LiteBox for user space or instead provide interfaces that let LiteBox consume COCONUT-SVSM as a platform. The group concluded that several questions must be resolved before deciding how strongly to commit to either model.
* **Shared Page-Table Requirements Need Clarification:** The TSC revisited making the page-table code generic for use by other projects, particularly LiteBox. More information is needed about LiteBox's requirements before choosing a direction.
* **Page-Table Changes Needed for User Mode:** Jörg said improved user-mode memory management, including `mmap`, `munmap`, and protection and remapping operations, requires substantial page-table changes.
* **Direct-Map Dependency Should Be Removed:** The current page-table implementation relies heavily on the direct map, which the project intends to remove. Mapping and unmapping should instead use the page-table self-map; this affects the design of any shared page-table crate.
* **Log Buffer Needs a Final Update:** The log-buffer PR still needs a rebase and a small update to continue printing messages to the console. Jörg said it should then be ready to merge.

### CocoonFS Persistence

* **CocoonFS PR Updated:** Nicolai updated the CocoonFS persistence PR after substantial work. He said only the final few commits differ from the version previously submitted, including documentation covering how to use it.
* **Review and Testing Requested:** Stefano plans to begin reviewing the PR, likely the following week, and will ask Arun to look at it as well. Testing from other contributors is also welcome.
* **Attestation Integration Is Follow-Up Work:** The implementation is not yet connected to attestation, which will be required for production use. The group agreed not to add that requirement to the already large PR before merging it.
* **Simpler API Can Be Added Later:** The current low-level API requires callers to create a transaction, stage updates, and commit it. Convenience helpers for common operations can be added later in either the CocoonFS crate or SVSM, particularly as user-space support is integrated.
* **vTPM Integration Is the Next Step:** The group discussed using CocoonFS as persistent storage for the vTPM. An existing helper can write a single file, while the vTPM's internal transactional NVRAM interface may also be connected directly to CocoonFS transactions to avoid unnecessary translation and buffer copying.
* **UEFI Variable Storage Also Planned:** After CocoonFS lands, persistence can also be wired into the UEFI variable store.
* **Persistence Remains a Major Priority:** Jörg said completing persistence is one of the project's highest development priorities for the year.
