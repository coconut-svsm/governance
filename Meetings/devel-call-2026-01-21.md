# Meeting Minutes: SVSM Development Call (January 21st, 2026)

## Topics:

### **TSC Update & Administrative Topics**

* **Google Summer of Code (GSoC):** The TSC discussed GSoC proposals; results have been posted to the mailing list. The deadline for submitting projects to QEMU is **January 30**.
* **Code Review Tools:** Experiments with GitHub "Code Owners" failed because GitHub does not auto-assign PRs to individuals without write access. The team is now exploring a CI script to parse a maintenance file for auto-assignments.
* **CCC Yearly Update:** Jörg will provide the annual project update to the Confidential Computing Consortium (CCC) Technical Advisory Council on **April 30, 2026**.
* **Upcoming Release:** A release is planned for next week, with several feature PRs currently being merged to meet the deadline.

### **Technical Discussion Points**

* **Persistent Storage (Cocoon-FS):** This remains a high-priority project. Progress is being made on the storage format specification review, with a goal to merge the code in the next few months.
* **User Space Allocator & `MMAP`:** Nicola identified a potential issue with the `MMAP` syscall draft regarding the use of **Object Handle 0**, which is currently used as an invalid value despite being a valid handle. Jörg noted that `MRESIZE` still needs to be implemented to allow the heap to grow.
* **KVM Planes Support:** Progress is expected to resume soon. Jörg plans to sync with Paolo to coordinate efforts and avoid duplicate work.
* **Rust Edition Update (2021 to 2024):** * The project is switching everything to the **2024 edition**.
  * Carlos clarified that all crates in the workspace will now inherit the Rust edition from the top-level `Cargo.toml` to avoid confusion with tooling like `cargo fmt`.
  * Because this change affects formatting across the entire codebase, **all open PRs will need to be rebased** once this is merged to ensure CI passes.
