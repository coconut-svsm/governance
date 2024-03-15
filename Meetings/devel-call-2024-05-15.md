# Meeting Minutes: SVSM Development Call (May 15th, 2024)

## Attendees:

Adam Dunlap, Carlos López, Chuanxiao Dong, Cláudio Carvalho, Ernestine Anderson, Huibo Wang, Jacob Xu, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Ramakrishna Gali, Roy Hopkins, Stefano Garzarella, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Document Sharing and Update Process:

* Joerg Roedel shared a development plan document for the SVSM project.
* The document will be placed in the public SVSM repository for version control and wider visibility.
* Updates can be submitted as pull requests (PRs).
* A link to the development plan will be added to the SVSM repository README file for easy access.

### Document Content:

* The document details the planned development work for the SVSM project.
* Discussion points included:
  * Tracking work assigned to individuals (decided to add to the document)
  * Prioritization of development tasks (to be added in future discussions)
  * File system calls (planned to initially cover real RAM files only, may be extended later)
  * CPUID instruction handling for x86 (implementation details discussed)
  * Asynchronous I/O and KVM support (potential need for protocol changes)
  * File system semantics vs. event system semantics (separate namespaces may be required)
  * Returning CPU cycles to the guest during SVSM I/O waits (requires protocol changes)
  * User space vs. kernel space considerations for file system access (needed for both)
  * FPU support for cryptographic operations (important for user space)
  * Build system support for multiple targets (e.g., ARM)
  * KVM support for AMD SEV-SNP and TDX partitioning (common interface for guest injection needed)
  * Memory isolation for SVSM (does not require separate KVM memory slots for AMD SEV-SNP and Intel TDX)
  * SVSM device interrupts (separate mechanism from KVM needed)
  * PDF document usefulness (table of content benefit acknowledged, GitHub Pages rendering capabilities to be explored)

## IGVM Changes for Intel TDX

* Peter Fang submitted a small fix to the SVSM IGVM branch in the QEMU repo and a larger PR is on the way.
* This is a first step towards being able to boot TDX VM. He reworked some of the TDX boot stuff and can now start the guest directly from a different entry point. Joerg Roedel suggests including instructions on how to put the firmware that gets included into the IGVM file.
* Roy Hopkins is about to upload a PR which reworks IGVM support and addresses a memory leak in a different way than Peter Fang's PR. They will coordinate their efforts to avoid merge conflicts.

## Measurement discrepancies

* Stefano Garzarella is finding a discrepancy between the launch measurement he has from the IGVM measure tool and the one he can see inside SVSM.
* Roy Hopkins suggests that the issue might be related to the restricted injection feature in QEMU. Stefano will investigate further.

## APIC driver

* Vijay Dhanraj asks if it's time to introduce the APIC driver since the restricted injection feature is being worked on.
* Joerg Roedel suggests coordinating with Jon Lange and his work on interrupt/IRQ dispatch which is also needed for TDX.

## Linux Plumbers Conference

* Cláudio Carvalho asks about the CFP deadline for the Confidential Computing microconference at the Linux Plumbers Conference 2024.
* Joerg Roedel says that the deadline is not known and they haven't even sent out a CFP yet. They will work on getting a CFP out soon.
