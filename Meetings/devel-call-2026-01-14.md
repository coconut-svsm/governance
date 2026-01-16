# Meeting Minutes: SVSM Development Call (January 14th, 2026)

## Topics:

### **Google Summer of Code (GSoC) Planning**

* **Umbrella Project**: The QEMU community is available to host SVSM projects as an umbrella organization, similar to how they handle Rust-VMM.

* **Project Ideas**:
  * The most promising ideas identified are **Observability** and **Device Tree support**.
  * Other ideas discussed previously included an SVSM bus, moving TPM to user mode, and various security-related tasks from the issue tracker.
* **Device Tree Support**: Luigi Leonardi is currently working on this and believes it is close to completion. He is willing to finish it himself or mentor a student if necessary.
* **Observability**: Jörg will follow up with Vasant and Nicola regarding the log buffer requirement, as there is an old pending Pull Request (PR) for this.
* **Next Steps**: Stefano will email the mailing list with GSoC details. Projects must be self-contained for a three-month duration and require at least one mentor.

### **Development & Repository Management**

* **`CODEOWNERS` File**: Tyler opened a PR to add himself to the `CODEOWNERS` file to receive notifications for relevant code changes. The team is investigating how to allow individuals without write access to be notified, potentially through GitHub CI.
* **Rust Import Styles**: There is ongoing discussion to reduce merge conflicts caused by Rust formatting.
* Jon Lange suggested a style of **one import per line with no braces** to minimize rebase conflicts.
* The "Linux style" (one import per line with braces and comment markers) was discussed but found to still result in conflicts after formatting.
* **PR Reviews**: The team briefly reviewed PRs related to the log buffer, the COCONUT allocator, and symbolized stack traces.

### **Technical Issues & Bug Reports**

* **KVM Boot Failure**: Carlos López and Oliver Steffen reported a boot failure under KVM when attempting to boot a full Linux image.
* The issue appears to occur when entering the guest at a lower VMPL on SEV.
* Jörg previously suggested waiting for specific pending PRs to land before revisiting this issue.
* **Action Item**: Oliver will follow up via email to clarify which PRs Jörg was referring to. The topic will be revisited next week when Jörg is present.
