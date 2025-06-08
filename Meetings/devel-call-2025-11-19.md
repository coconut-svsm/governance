# Meeting Minutes: SVSM Development Call (November 19th, 2025)

## Topics:

### **Technical Steering Committee & PR Process**

* **PR Review Protocol:** Stefano summarized the recent Technical Steering Committee discussion regarding the review process. Since GitHub automatically adds code owners as reviewers, the team will utilize the "assignees" feature to designate the specific required reviewers for a Pull Request (PR).
* **Assignee Role:** Anyone listed as an assignee is considered a required reviewer.
* **Internal Coordination:** Jon clarified that the assignees feature is primarily for the Technical Steering Committee to coordinate required reviews among themselves; external contributors should still request reviews via the traditional reviewers section.

### **Development Updates**

* **LibTPM:** The team has begun improving the build process for LibTPM and is looking into splitting components to better understand the structure.
* **Allocator Trait:** Joerg is communicating with Carlos and Vaishali regarding the allocator trait and implementing fallible allocations.
* **Reset/Reboot Support:** Joerg is managing the reset/reboot PR in contact with Richard, though discussions regarding the full TPM reset are ongoing.

### **Hypervisor and Firmware Support**

* **IGVM and QEMU:** Thanks to Oliver, the MADT table is now provided via IGVM for all supported hypervisors, including QEMU.
* **QEMU Updates:** The QEMU changes have been merged, and team members need to update their local QEMU versions.
* **Firmware Config (fw_cfg):** The goal is to reduce the usage of the QEMU firmware config. It is currently still needed for VirtIO devices, but future support will rely on Device Tree and IGVM.

### **Verus Library & Dependencies**

* **Crates.io Migration:** The Verus team has released their library to crates.io.
* **Verification:** Ziqiao has opened a PR for this update.

### **CI and Verification Workflow**

* **Manual CI Trigger Proposal:** Ziqiao proposed adding a manually triggered CI workflow for verification to assist reviewers who may have trouble setting up the environment locally.
* **Local Verification Priority:** Jon argued against relying on CI for verification at this stage, emphasizing that developers should maintain the ability to run verification locally to ensure they understand the syntax and tools.
* **Resource Usage:** It was noted that if verification is not automatic, it is more efficient to run it locally rather than using server CPU cycles.
* **Documentation:** The team agreed that local configuration documentation needs to be kept up to date so anyone can run the verifier.

### **Action Items**

* **Stefano Garzarella:** Will review and test Ziqiao’s PR regarding the Verus library dependency update.
* **Ziqiao Zhou:** Will create a GitHub issue or PR to document the proposal for the manual CI verification trigger for further discussion by the steering committee.
