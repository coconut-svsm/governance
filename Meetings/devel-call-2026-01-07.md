# Meeting Minutes: SVSM Development Call (January 7th, 2026)

## Topics:

### **General Updates & TSC Summary**

* **TSC Meeting Recap**: The Technical Steering Committee (TSC) met on January 6 to discuss project updates, technical issues, and maintenance models.
* **Kernel Memory Layout**:
  * There was a proposal to move SVSM into the 32-bit GPA space to simplify AP (Application Processor) bring-up.
  * **Conclusion**: This change is not currently feasible but will be reconsidered once the IGVM memory map work is complete.
  * **Current Status**: SVSM currently resides at 64MB GPA on Hyper-V and at the 512GB boundary on QEMU.
* **Submaintainer Model**:
  * The team is exploring a submaintainer model due to GitHub's requirement that "CODEOWNERS" have full write access, which is currently limited to TSC members.
  * **Proposed Solution**: Researching GitHub Actions to automatically assign reviewers based on the specific files modified in a PR.

### **Rust Edition 2024 Update (PR #934)**

* **Decision**: The project is moving forward with updating the Rust edition to 2024.
* **Implementation**:
  * The update will include a project-wide formatting change in a single commit to maintain CI respectability.
  * Carlos used automated tooling to handle most breaking changes, followed by manual reviews to minimize unnecessary diffs.
* **Compatibility**:
  * Current toolchains (Rust 1.86 minimum) already support both the 2021 and 2024 editions, so no major issues are expected for downstream consumers.
  * Luigi Leonardi (Fedora maintainer) will test PR #934 before it is finalized.
* **Formatting Discussions**:
  * The team discussed adopting the Linux kernel's vertical import formatting (using trailing double slashes) to minimize rebase conflicts.
* **Conclusion**: While it causes "short-term pain," the codebase is still small enough to manage a full conversion if decided.

### **Pending PRs & Next Steps**

* **PR #900**: This PR will be prioritized for merging before the Rust edition update to ensure Linux boots correctly.
* **Testing**: Jörg Rödel will conduct more intrusive and extensive testing on the Rust 2024 changes before they are fully integrated.
