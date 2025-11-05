# Meeting Minutes: SVSM Development Call (October 29th, 2025)

## Topics:

### **Technical Steering Committee (TSC) Meeting Update**

* **October Development Release**
  * The October development release was checked and generally looks good.
  * **Breakage:** Formal verification is currently broken.
    * This is likely due to the verifier not yet supporting a newly used feature, possibly "Raw Borrows".
    * An [issue](https://github.com/coconut-svsm/svsm/issues/840) has been created and tagged for a fix.
  * **Improvements:** The release includes improvements in stack usage, memory, and **MMIO support for native**.
* **Policies Review Status**
  * The policy documents will remain open for review until the beginning of next week.
  * Attendees were encouraged to review and comment on the pending PRs.
  * The policies are expected to be **merged into the governance repository** early next week if no major objections are raised.
* **CODEOWNERS Files**
  * The TSC discussed adding `CODEOWNERS` files to most repositories in the **COCONUT-SVSM GitHub project** (excluding a few downstream forks).
  * **Action for Maintainers:** Maintainers of non-downstream repositories (including the SVSM repository) should expect or are welcome to submit a PR to add a `CODEOWNERS` file.
  * The file should be placed in the **repository root** (not the `.github` directory).
  * Code owners should be listed using **email addresses** rather than GitHub usernames for ease of contact.
* **Dependency Management**
  * Work is ongoing to establish a dependency management system for SVSM.
  * This work includes addressing issues related to **Dependabot PRs** for updating dependencies with security concerns.
* **Google Summer of Code (GSoC) 2026**
  * **Decision:** The project will **attach itself to the QEMU project** for GSoC 2026, as QEMU offered to host them this year.
  * The goal is to mentor approximately **two projects** next year.
  * **Next Step:** The team will reach out to the QEMU project to determine the necessary application requirements.
* **SVSM Demo Review**
  * A demo prepared by Oliver and Stefano was presented.
  * The demo showcased the full stack of an **SVSM with a persistent TPM and working disk unlock**.
  * **Action:** The team will further review the demo to identify components that should be **integrated into the main SVSM repository**.

### **SVSM Memory Allocation Discussion**

* **Fallible vs. Infallible Allocation**
  * **Topic:** Is the currently planned implementation of **fallible allocations** sufficient, or should tasks that fail memory allocation be put **to sleep**? 
  * Putting a task to sleep could eliminate the need to instrument all code paths for failure handling.
  * **Context:** SVSM's ability to get more memory (e.g., asking the guest via SVSM protocol) depends on the use case, making sleeping potentially unviable in some scenarios.
  * **Conclusion:** The TSC did not reach a conclusion and requires **more discussion** with the wider group.
* **OOM Risk Assessment**
  * The team discussed whether OOM is a practical concern in SVSM, given that most memory is pre-calculated and allocated at boot time.
  * It was noted that while memory is mostly boot-time allocated, structures like the **bitmaps for run-length encoding** are dynamically allocated at runtime, though the current memory consumption is small.
  * The need to prepare for OOM situations, primarily to prevent exploits from memory leaks.
* **Proposed Path Forward**
  * **Proposal (Nicolai Stange):** The project should use the experimental allocator API to implement the allocator as **infallible for now**.
    * This approach meets the objective of simplifying error handling.
    * Once the allocator API is stabilized, a **fallible allocator** can be introduced later for larger allocations if a practical need arises.
  * **Agreement:** Jörg Rödel agreed that this approach is a simple and good way to proceed.
