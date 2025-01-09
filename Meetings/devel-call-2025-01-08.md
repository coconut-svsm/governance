# Meeting Minutes: SVSM Development Call (January 8th, 2025)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Jean, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Lendacky, Vasant Karasulli

## Topics:

### Release Process

* Joerg Roedel proposed a monthly development release cadence with a one-week stabilization period where only bug fixes are merged into the main branch.
* Jon Lange and Dionna Glaze expressed concerns about the proposed stabilization period, suggesting it could hinder feature development and create merge conflicts. They recommended using release branches instead.
* James Bottomley suggested releasing a development version first and then evaluating the number of bugs to determine the appropriate stabilization time.
* Joerg agreed to release a development version this month and reassess the process based on the experience.

### IGVM QEMU Support

* Joerg Roedel inquired about the status of Roy Hopkins' IGVM QEMU support patches.
* James Bottomley noted that the patches have been inactive since September and require reposting.
* Stefano Garzarella volunteered to take ownership of the patches, ping Daniel for feedback, and repost them.
* Roy Hopkins joined the call and confirmed he will address any outstanding comments and repost the patches.

### Restricted Injection

* Jon Lange asked about requiring restricted injection in KVM for COCONUT.
* Tom Lendacky clarified that restricted injection is currently only in the COCONUT branch of KVM, not upstream.
* Joerg Roedel agreed to review the KVM patches and determine if restricted injection can be safely required.

### Multi-VMPL Interrupt Support

* Jon Lange raised concerns about the lack of multi-VMPL interrupt support in QEMU/KVM and its impact on interrupt usage in COCONUT.
* Joerg Roedel suggested introducing a hypervisor check to work around the issue until KVM supports multi-VMPL interrupts.
* Tom Lendacky confirmed that Roy Hopkins' patches direct all interrupts to the lower VMPL, effectively disabling interrupts for the SVSM in QEMU.
* The group agreed to use a hypervisor check to disable interrupts for SVSM in QEMU and revisit this once KVM has proper multi-VMPL interrupt support.

### TDX Updates

* Peter Fang provided an update on TDX, stating that he pushed a new PR to the Linux repo to restore TDX patches.
* He mentioned that IGVM support for TDX will require upstreaming basic TDX support in QEMU first.
* Peter questioned whether pre-building page tables in IGVM is necessary for TDX startup.
* Jon Lange explained the challenges with pre-building page tables in IGVM for both SNP and TDX, mainly due to the unknown location of certain bits until runtime.
* Peter agreed to implement TDX stage one changes without pursuing stage2 modifications for now.

### Stage2 Discussion

* Jon Lange and Joerg Roedel discussed the long-term goal of minimizing or eliminating stage2.
* They acknowledged challenges related to memory layout and the need for changes in SVSM, IGVM builder, and OVMF.
* Jon Lange emphasized the need for OVMF to learn about memory layout from the SVSM, potentially through IGVM memory parameters.
