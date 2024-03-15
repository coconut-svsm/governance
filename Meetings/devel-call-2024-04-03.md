# Meeting Minutes: SVSM Development Call (April 3, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, David Altobelli, Dionna Glaze, Huibo Wang, Jacob Xu, James Bottomley, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay dhanraj

## Topics:

### vTPM Merge and Issues:

* Joerg Roedel merged the vTPM PR, causing build issues for some.
* Roy Hopkins identified a linking issue related to stage 2 builds.
* Cláudio Carvalho reported another issue with vTPM and Microsoft TPM.
* Discussion on using OpenSSL 3 vs. maintaining a fork of Microsoft TPM due to
  code size increase and maintenance overhead.

### Security Issues:

#### General:

* A security researcher reported five issues related to race conditions in handling SVSM core protocols.
* Joerg Roedel proposed mitigation strategies and gathering feedback for potential side effects.
* Jon Lange suggested using a mutual exclusion lock to prevent race conditions.
* Joerg Roedel decided to use a lock instead of zeroing out pages.

#### Double PValidate (Tom Dohrmann):

* Tom inquired about mitigating reported race conditions causing double pvalidation of memory
* Joerg Roedel explained the challenges and potential solutions, including tracking validation status of pages, which is resource-intensive.
* Mitigation will take some time as some trade-offs need to be made
* They agreed to document the issue for user awareness.

### PR Updates:

* Vijay dhanraj inquired about merging a PR to update SVSM Linux repository.
* Joerg Roedel clarified that the recommended branch is `svsm` and explained the inactive PR can be closed.
* Vijay dhanraj also asked about updating the non-IGVM branch in the QEMU repository. Joerg explained the deprecation of non-IVGM code.

### Early Attestation Document:

* Stefano Garzarella announced starting a document for early attestation and shared access with Roy and Oliver.
* He plans to send a mailing list email with the link for wider discussion. [Link](https://docs.google.com/document/d/11ZsxP8jsviP3ddp9Hrn0rf6inttNw_Pbnz0psXlxlPs)
* Agreed to move the document to a markdown file in a Github repository and update via PRs once in a good state.

### User Mode Support:

* Joerg Roedel shared progress on user mode support, achieving the ability to load and execute ELF binaries.
* He submitted a PR for review and welcomed feedback.

### Update Process for Linux and QEMU Repositories

* Vijay dhanraj inquired about the process to update QEMU and Linux kernel support repositories for COCONUT-SVSM
* Joerg Roedel clarified there's no set schedule for updates.
* Updates happen on a best-effort basis and as new versions of the non-upstream patch-sets become available
* Acknowledging that updates are primarily for development purposes for now; older versions may suffice.
* Updating to the latest version might be necessary for specific features (e.g., TDX enablement).
* Re-basing QEMU to the latest version might be easier than updating for TDX support.
* Merging updates might involve resolving conflicts between SNP and TDX patches.
