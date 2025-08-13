# Meeting Minutes: SVSM Development Call (August 6th, 2025)

## Topics:

### Technical Steering Committee (TSC) Update

* This is being introduced as a regular agenda item to increase transparency.
* TSC will not meet for the next week and in three weeks due to vacations.
* General Maintainer Workflow: A discussion was held regarding a mistake where a review comment suggestion was committed, causing the CI to fail due to missing a signed-off commit. The conclusion was to avoid pushing to other people's branches in pull requests (PRs) in the future, except for minor fixes.
* IGVM Memory Map Support for OVMF: Jörg provided an update that work is being done on this.
  * The proposed approach is to use the IGVM interface to create an IGVM memory map in the SVSM and place it at an expected location for OVMF to pick up.
  * The reasoning is that this would also help a non-SVSM setup (e.g., a VMPL0-only guest) and align with how the hypervisor would communicate with OVMF.
* PR [#774 (TPM Bindings)](https://github.com/coconut-svsm/svsm/pull/774): This PR was mentioned as needing review.
* GitHub Milestones: For the September development release, the team will try using GitHub milestones in parallel with the current tag system to see which is more effective for tracking issues and PRs.

### Dynamic Device Discovery

* This discussion arose from the pending VSOCK interface PR.
* Problem Statement: When the SVSM boots, it needs a way to dynamically discover the devices and service capabilities provided by the hypervisor (e.g., VSOCK and serial devices, MMIO, block device attachments).
* Current Issue: Currently, the SVSM expects a static set of devices. If a device is not present, boot can fail. This is not a desirable solution and should be more dynamic.
* **Proposed Solution**: Jon Lange and Chris Oo suggested using a "device-tree" for this purpose. Jon noted that this is a natural choice because Linux already understands device trees for configuration, and the IGVM file format supports a parameter type for this.
* Chris Oo added that the reasons for choosing a device tree are its flexibility and ease of parsing and generation.

### Upcoming Release

* Jörg mentioned that he had prepared an upcoming release.
* The pull request (PR) for this is pending, but he will push the commits directly to ensure the Git tag is properly pushed to the repository.
* He expected this to happen "tomorrow morning" and that the project would most likely see its first development release then.

### Undocumented Unsafe Blocks

* Stefano announced that the work on documenting all unsafe blocks in the project is now finished and the clippy lint has been enabled.
* Jörg confirmed this and both thanked everyone who was involved in making this happen.
