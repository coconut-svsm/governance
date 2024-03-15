# Meeting Minutes: SVSM Development Call (February 12th, 2025)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Geoffrey Ndu, Hajira Zaman, Huibo Wang, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tom Lendacky, Vasant Karasulli, Ziqiao Zhou

## Topics:

### Announcements:

* Thanks to Dionna, the project now has an official logo available in the [CCC artwork repository](https://github.com/confidential-computing/artwork/tree/main/coconut_svsm).
* CCC Project Update: The COCONUT-SVSM project update to the Confidential Computing Consortium (CCC) is scheduled for June 12th.

### Pull Requests:

* Discussion of open attestation PRs from Tyler and Geoffrey, and the differences in their approaches.
  * Action item: Joerg to review open PRs and provide feedback.
* Discussion of IGVM patches for QEMU and the upcoming QEMU 10 release.
  * Action item: Someone to pick up, rebase, and repost the IGVM patches. Stefano to reach out to Roy regarding the patches.
* Discussion of PR 614 (native platform running on QEMU 64) and its reliance on IGVM patches.
* Discussion of PR 547, updated by Peter Fang. Joerg will review.

### Rust Standard Library Support:

* Update on a MSFT Rust expert's progress in building an init task using standard Rust that runs in user mode.
* Discussion of the need for a Rust target for the COCONUT-SVSM and the challenges of upstreaming Rust changes.
* Discussion of tier 3 target status in Rust and the potential need for a temporary private compiler fork.

### VirtIO-Blk and DMA:

* Oliver Steffen raised questions about the VirtIO drivers crate, MMIO base addresses, and shared box buffer structure.
* Discussion of DMA API, allocation sizes, and potential software IOTLB implementation.
* Discussion of how to configure the base address and differentiate between devices for the SVSM and guests. QEMU FWCFG is a temporary solution.

### OVMF and Memory Management:

* Discussion of OVMF consuming the SVSM range described in the SEV-SNP secrets page.
* Discussion of a unified architecture for memory discovery between TDX and SNP.
* Discussion of the need for dynamic memory allocation and page validation bit map for the SVSM.

### Unsafe Blocks:

* Discussion of the goal of trending towards zero uncommented unsafe blocks.
  * Action item: Joerg to look at the memory management side and document unsafe blocks.
* Stefano to continue work on documenting unsafe blocks related to services.

### CCC Kernel SIG Meeting:

* Announcement of the CCC Kernel SIG  meeting on the next day to discuss a generic communication interface between confidential guests and SVSM.
  * Details are in the [CCC Calendar](https://zoom-lfx.platform.linuxfoundation.org/meetings/ccc?view=week)
* Joerg to send an email to the SVSM mailing list with meeting details.

### CI Issues:

* Discussion of CI failures related to publishing documentation.
* Stefano to resolve the CI issue in PR 606.
