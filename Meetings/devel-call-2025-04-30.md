# Meeting Minutes: SVSM Development Call (April 30th, 2025)

## Topics:

### Announcements:

* The meeting will be moved to the Confidential Computing Consortium (CCC) Zoom instance (Linux Foundation Zoom instance) starting next week.
* Details will be sent via email, and a PR will be submitted to update the governance repository.
* Participants will likely need a Linux Foundation account.
* The old mailing list will be shut down in approximately two weeks, and everyone should subscribe to the new one.

### Pull Request Reviews:

* Oliver Steffen requested reviews on the VirtIO pull request, which includes a feature flag to disable the driver.
* Another PR related to running QEMU in non-confidential mode for SVSM boot testing also needs review.
* Joerg Roedel will test these PRs after updating his test machine.

### EDK2 Memory Fragmentation:

* Adam Dunlap reported an issue with EDK2 not freeing CAA pages, leading to a fragmented memory map.
* Discussion centered on whether CAA pages should be freed after ExitBootServices and potential issues with downstream modifications.

### vTPM Build Issues:

* Joerg Roedel discussed a PR addressing missing `stddef.h` errors in the vTPM build, which caused make test to break.
* The addition of libcrt include directory fixed the build for Joerg, but the reason it was not there initially is not clear.
* Dionna Glaze suggested potential solutions including using `-I system` instead of `-I` and potential conflicts when linking against two C libraries.
* Discussion also addressed testing of the vTPM module.

### Rust Update:

* Dionna Glaze discussed a PR to update Rust from 182 to 1.84.1, which addresses linter and clippy failures and enables access to the strict providence feature.
* Joerg Roedel suggested updating to 1.186 in a follow-on PR.

### Specification Work:

* Tom Lendacky is working on the SVSM specification.

### Memory Verification in Allocator Module:

* Ziqiao Zhou introduced a large PR to add memory verification in the allocator module.
* includes ghost and trackable memory permissions.
* Feedback was requested on readability and annotations.

### VM Firmware Update Interface:

* Dionna Glaze mentioned the CCC Kernel SIG meeting on May 8th to discuss the VM firmware update interface (FUKI) concept and the need for hypervisor implementers to agree on virtual device interfaces.
* Discussion centered on using IGVM as a standard format for loading firmware and what is missing from IGVM to handle the special reset semantics for the VM firmware update interface.

### vTPM Service and Soft Lockups:

* Dionna Glaze raised concerns about potential soft lockups in the Linux kernel when generating keys for the vTPM service.
* Discussion addressed the execution model of SVSM, where vCPUs are dropped from the Linux kernel, and potential solutions, including updating the SVSM perform call protocol, yielding in the vTPM code, and pre-caching RSA 2048 keys.
* James Bottomley suggested short term band-aids while a more long term solution for preemption in the vTPM code is explored.
