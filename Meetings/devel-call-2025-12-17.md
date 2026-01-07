# Meeting Minutes: SVSM Development Call (December 17th, 2025)

## Topics:

### **Administrative Updates**

* **Final Call of the Year:** This meeting serves as the last SVSM development call before the holidays.
* **Schedule Resumption:** The next call is scheduled for January 7th; there will be no calls during the holiday break.

### **TSC Meeting Recap**

* **Group Dynamics:** The TSC agrees the group is working well together, with processes in place that support project quality and steady progress.
* **Upstream Adoption:** A major identified issue is the lack of upstream adoption, primarily due to the SVSM project not being consumable upstream yet because of missing KVM support.

* **Priorities for Next Year:**
  * **KVM Support:** Continuing to look into KVM support is a main item for the upcoming year.
  * **Persistent Support:** Implementing persistence support in the SVSM is a high-priority critical feature for consumers.
  * **Merge Velocity:** The group aims to improve the PR review process to reduce the time PRs remain open.
  * **Hardware Support:** There is a goal to steer the project toward supporting more hardware platforms.

### **Plumbers Conference Highlights**

* **Live Migration:**
  * Discussions focused on the path toward live migration, which is a highly requested feature.
  * Missing components include KVM plane support and SVSM page state tracking (tracking states for the whole VM, not just the SVSM).
* **SVSM Specification:** AMD plans to spend time determining how to move the SVSM spec into the community.
* **Alternate Injection:** Melody provided an update on alternate injection work, which touches the SVSM project.
* **Rust for Linux:** The experimentation phase is over, and the kernel community is committing to moving forward with Rust, potentially accepting Rust-only drivers in the future.

### **Technical Discussion: Rust Allocators & Kernel Collaboration**

* **Collaboration Attempt:** Jörg Rödel discussed sharing allocator code (specifically fallible allocations) with the Rust-for-Linux team.
* **Technical Challenges:**
  * **Memory Models:** The Linux kernel follows the C++ memory model (using their own atomic implementations), while SVSM uses the standard Rust memory model and atomics.
  * **Configuration:** The kernel requires different allocation flags than SVSM.
  * **Doc Tests:** The kernel integrates doc tests into the KUnit infrastructure using internal kernel allocators. Moving code to a separate crate breaks these tests because they rely on the kernel crate.
* **Proposed Strategy:**
  * It was decided not to pursue a joint implementation immediately due to the need for high configurability.
  * The plan is to start a separate crate (fork), potentially asking the kernel team to change the license to MIT/Apache or factor out the code they can.
  * SVSM will consolidate the code for its own needs first. Convergence with the kernel codebase may be revisited later.
* **Action Item:** Vaishali will organize a forum with the kernel team after the holidays to discuss licensing and the possibility of factoring out code.

### **TDX Partitioning Support**

* **Status Update:** Updates on TDX partition support have stalled.
* **Blockers:**
  * There is no meaningful support for TDX partitioning upstream in KVM.
  * There is no published protocol for TDX analogous to the SVSM protocol defined for SNP.
* **Path Forward:**
  * Progress is demand-driven; foundational support in KVM for multiple privilege levels (planes) is a prerequisite.
  * Interested parties should reach out to Peter Fang to discuss use cases (e.g., vTPM) and potential implementation paths.
