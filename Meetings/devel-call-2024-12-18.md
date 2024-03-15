# Meeting Minutes: SVSM Development Call (December 18th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, James Bottomley, Joerg Roedel, Jon Lange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tyler Fanelli, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Linux Kernel and QEMU Repository Updates

* Joerg Roedel reminded everyone to test the new branches of the Linux kernel and QEMU repositories.
* The changes were necessitated by the introduction of TPR usage in the SVSM.
* Peter Fang was asked to check and resubmit any changes that might have been accidentally removed from the `svsm-tdx` branch in the Linux kernel repository.

### TDX Multiprocessor Startup

* Jon Lange discussed his draft PR for multiprocessor startup for the non-isolated native platform, which utilizes `INIT` and `SIPI`.
* He highlighted the similarities between the challenges in native multiprocessor startup and TDX startup, suggesting the possibility of sharing code between the two paths.
* Peter Fang expressed interest in the draft PR.
* Jon Lange also mentioned the upcoming IPI-based vCPU TLB-flush functionality.

### Unsafe Block Detection

* Jon Lange raised concerns about the ongoing challenge of addressing unsafe blocks in the codebase, particularly in the context of CI and clippy lints.
* Stefano Garzarella reported progress in reducing unsafe blocks in the vTPM module.
* Joerg Roedel agreed to help with reviewing and documenting unsafe blocks, particularly in the memory allocator, in January.
* A discussion ensued about setting a deadline for documenting all unsafe blocks, with the possibility of setting a goal of the end of February.

### vTPM Attestation and EK Template

* Cláudio Carvalho initiated a discussion about the choice of EK template for generating the EK in the vTPM attestation protocol.
* James Bottomley advocated for using ECC P-256 due to its superior security and efficiency compared to RSA-2048.
* The possibility of supporting multiple EK pubs and configuring them at build time was discussed.
* James Bottomley suggested specifying the algorithm as part of the attestation report to address potential compatibility issues.
* Tyler Fanelli noted that Keylime has support for ECC P-256.

### UUID Implementation

* Cláudio Carvalho inquired about the possibility of using the external UUID crate instead of the internal implementation.
* Stefano Garzarella mentioned the UUID dependency in the `igvmmeasure` tool.
* Joerg Roedel agreed to investigate the external crate and compare it with the existing implementation.

### SVSM Observability for TDX

* Peter Fang provided an update on the discussions with Elena regarding SVSM observability for TDX.
* He mentioned the need to convince Linux architects about the use case and gain their approval for adding the necessary infrastructure.
* Jon Lange offered to assist in convincing the relevant stakeholders.

### SVSM Memory Allocation

* Adam Dunlap proposed a small feature to address the issue of variable memory requirements for the SVSM region.
* The idea involves having the hypervisor guess the required memory and pass the allocated amount to the SVSM via an IGVM command line parameter.
* Jon Lange suggested an alternative approach using device tree as an IGVM parameter to specify memory that is not exposed in the E820 map.
* Adam Dunlap agreed to explore this approach and potentially submit a PR.

### SVSM Memory Management

* Jon Lange raised a concern about the potential need for a real heap in the SVSM memory manager to handle discontiguous memory regions.
* Joerg Roedel acknowledged this as planned work for the future.

### User-Space Support PR

* Vijay Dhanraj reminded Joerg Roedel about the user space support PR and requested a review.
* Joerg Roedel confirmed that it is on his list of things to review before the holidays.

### Year in Review and Outlook for Next Year

* Joerg Roedel expressed gratitude for everyone's contributions and highlighted the achievements of the project in the past year, including:
  * Merging VTPM
  * Extending hypervisor support
  * Basic support for TDX and other platforms
  * Progress with user mode HVM support
  * Nearing completion of IPI support
  * Joining the Confidential Computing Consortium
* Joerg Roedel outlined the following goals for the next year:
  * Completing persistent memory and attestation support
  * Further improving hypervisor and multi-platform support
  * Making progress on KVM support
  * Moving closer to supporting para-virtualized workloads
  * Establishing a Technical Steering Committee
  * Making the first release of the project

###  Closing Remarks

* Joerg Roedel thanked everyone again and wished them happy holidays.
* The next meeting was scheduled for January 8th.

