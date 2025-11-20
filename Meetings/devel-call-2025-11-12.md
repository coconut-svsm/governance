# Meeting Minutes: SVSM Development Call (November 12th, 2025)

## Topics:

### **TSC Meeting Update**

Jörg Rödel provided an update from the previous day's TSC meeting:

* **Development Plan PR:** Discussed a pending Pull Request (PR) for the development plan.
  * **Goal:** To label items in the plan to identify suitable projects for Google Summer of Code (GSoC) (e.g., 3-month projects) and "good first issue" tasks for newcomers.
  * **Action Item:** The PR is open for review until the end of the week, after which it will be merged if there are no major objections.
* **Google Summer of Code (GSoC) Process:**
  * **Mentors:** Mentors are needed for the identified projects.
  * **Next Steps:** Once the plan is ready, they will start asking for people willing to mentor.
* **Development Plan Location:** Discussed whether the Development Plan should be in the SVSM repository or the governance repository.
  * **Reason to Keep in SVSM:** James Bottomley suggested keeping it in the development repo increases the chance of contributors updating it when fixing things or adding features.
  * **Decision:** It was agreed to consider keeping the document in the SVSM repo, acknowledging this point.
* **Repository Policy and CI Updates:** Repositories are being updated according to policies merged last week.
  * All repos now have a `CODEOWNERS` file.
  * Basic CI checks for DCO (Developer Certificate of Origin) on new commits.
  * Rust-based repos have added quality checks (`rustfmt`, `clippy`).
* **Build System Changes:** Ongoing work to change the build system to place build artifacts in a separate directory outside the source tree, which allows an update to the `.gitignore` file.

### **Reset-Reboot Protocol PR Discussion (Richard Relph & Jörg Rödel)**

* **vCPU State Clarification:** Jörg Rödel requested clearer specification on the vCPU state post-reboot, specifically if all vCPUs at the calling VMPL (registered VMSAs) are reset to the init state.
  * Richard Relph noted his current implementation only resets the state of the BSP (Boot Strap Processor), which appears sufficient for graceful Linux reboots.
* **Crash/Unexpected Reset Scenario:** James Bottomley and Jörg Rödel raised concerns about unexpected resets (e.g., from a guest crash) where the kernel may not have shut down all APs (Application Processors) correctly.
  * Leaving other vCPUs running while the SVSM begins memory invalidation could cause faults, a VM crash, or security issues.
  * Jörg suggested the SVSM would need IPIs (Inter-Processor Interrupts) to force running vCPUs into VMPL 0 and shut them down.
* **Memory Invalidation Description:** Richard Relph clarified his spec states that the reboot invalidates *only* memory pages that were validated by the guest, not all memory.
* **OVMF Metadata:** Jörg suggested Richard could find the memory regions OVMF expects to be valid in the SEV metadata within the OVMF image, located on the page below the VMPL2 boot vector.
* **Action Item (Specification):** James Bottomley suggested the spec should state that the APs are properly quiesced as they would be on first boot.
    * Jörg Rödel will write an updated sentence for the specification, limiting the state restoration to the **vCPU and guest memory state** to match that of a newly booted guest.
* **Conclusion:** The group agreed to first finalize the specification and then proceed with the PR.
