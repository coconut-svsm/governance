# Meeting Minutes: SVSM Development Call (March 25th, 2026)

## Topics:

### **Technical Steering Committee (TSC) Update**

* **Topics Discussed**:
    * **PR Merges**: The heap changes PR was recently merged.
    * **Clippy Setup**: The team reviewed the setup involving four different Clippy modes and clarified the use of `RUST_FLAGS`.
    * **Memory Management**: Future changes to the memory management system were discussed, specifically whether to use `struct VMR` for both user and kernel modes.
    * **Security Features**: Proposed features such as KPTI, KCFI, and KASAN were reviewed; however, the current decision is not to implement these for now.
* **Decisions**:
    * The team will review the usage of `struct VMR` in kernel mode, as it is currently only used for per-CPU memory.
    * The global issue tracking security features (Issue 448) will be closed. New, specific issues will be created for individual features the team decides to pursue.

### **Upcoming March Release**

* This week is release week for the March development release.
* Testing is currently underway, including running fuzzers, and results look positive so far.
* Jörg intends to complete the release by the end of the week if testing remains successful.

### **GitHub Workflows and CI Updates**

* **PR 1013**: This PR aims to further limit workflow permissions (specifically for `PublishDocs`) and address unpinned dependencies.
* **Dependency Management**: 
    * To fix an unpinned `pip install` issue, the Python environment will now be installed via Ubuntu packages.
    * The manual verification workflow was changed to download a specific commit ID and build it during the workflow rather than using a pre-built binary.

### **CI Failures and Caching**

* A recent CI failure in one of John's PRs was traced to repository corruption caused by GitHub overwriting the `tools` directory with a cached version of QEMU.
* The team agreed that caching should not occur inside the repository checkout.
* The cache will be moved to a separate directory once PR 1013 is merged.

### **Stale GitHub Branches**

* James Bottomley reported concerns from the community regarding "stale" branches in subordinate projects like the kernel, QEMU, and EDK2.
* **Decisions/Plans**:
    * **QEMU**: A rebase of downstream changes to QEMU 11 is planned, which should help clean up the tree.
    * **Kernel**: The team is currently waiting for "Planes" before moving to a continuous rebase model.

### **Issue 399 - Virtual Platform Attestation Protocol**

* **Context**: The issue relates to specific workflows potentially planned for GCP.
    * Jörg Rödel asked for the current state of the issue and whether it is still required.
    * Adam Dunlap noted that attestation is currently handled by his colleague.
    * The issue is quite old, and a new "single-service attestation" is expected to be coming soon.
* **Action Items**:
    * Adam Dunlap to direct his colleague to the issue to provide a status update or comment.
    * The team will consider closing the issue based on the forthcoming comment.

### **Emulated Attestation for Native Mode**

* Luigi Leonardi proposed introducing emulated attestation for native mode to facilitate testing in Continuous Integration (CI).
* **Points Raised**:
    * Jörg Rödel agreed it is useful but suggested waiting for discussions with the IGVM core teams.
    * There is a shift toward moving expected launch measurement calculations into the IGVM crate itself.
    * A decision is needed on whether to adopt Hyper-V's VSM measurement style or create a unique method.
    * Luigi suggested that a simple "fake" or injected measurement might suffice for testing purposes.
    * Jörg noted that even in native mode, where the hypervisor is trusted, a measurement can provide proof to a guest owner that the correct IGVM file was loaded.
* **Action Items**:
    * Wait for updates from the IGVM group following their scheduled discussion on **April 8th**.

### **Scheduling and Logistics**

* Europe is switching to summertime (Daylight Saving Time) next weekend.
* For participants in the US, the meeting will return to its original scheduled time starting next week because the meeting is anchored to a European time zone.
