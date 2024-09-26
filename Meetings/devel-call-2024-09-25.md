# Meeting Minutes: SVSM Development Call (September 25th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Diego Gonzalez Villalobos, Dionna Glaze, James Bottomley, Joerg Roedel, Jon Lange, Nicolai Stange, Peter Fang, ramakrishna gali, Roy Hopkins, Tom Dohrmann, Tom Lendacky, Vijay Dhanraj

## Topics:

### LPC and KVM Forum Updates:

* Microsoft's OpenHCL: Microsoft announced OpenHCL, a Rust-based paravisor running in user space based on the Linux kernel. COCONUT aims to integrate OpenHCL user-space to provide identical functionality.
* `Guest_memfd` and Confidential Computing: Discussions at LPC and KVM Forum focused on `guest_memfd`, TD-partitioning, and ARM-CCA planes. COCONUT plans to run on these platforms as well.
* COCONUT-SVSM BoF: Secure Storage and Identity Provisioning for SVSM: The meeting discussed secure storage and identity provisioning using vTPM.
* Discussion around vTPM and persistence:
  * Proxy whether network stack in SVSM
  * No network stack, proxy can run in a side VM to get network access - transparent for SVSM
  * KBS Protocol Driver: Dionna Glaze suggested writing a simple driver for the KBS protocol and iterating on it.
  * Qemu Prototype: Dionna Glaze proposed writing a Qemu prototype, and CSPs would provide drivers.
* KVM Features: The meeting discussed necessary KVM features for COCONUT's success, including vTOM on AMD, VMSA settings and VMPL support.
* VM Privileged Levels: There were discussions about privilege levels in KVM, with a focus on efficient switching mechanisms. A new architecture is being proposed to address these requirements.
* Secure IRQ Delivery: AMD presented on secure IRQ delivery for SEV-SNP
* Live Migration: Meeting discussed options for live migration using SVSM.

### Stage 2 Split:

* Stage 2 Splitting: Tom Dohrmann proposed splitting Stage2 into a separate crate.
* Some challenges around page validation in stage2:
  * `virt_to_phys()` and `phys_to_virt()` unreliable in stage2
  * Jon Lange noted that the temporary mapping facility is missing in Stage 2 for SNP platforms which would help preventing the use of `phys_to_virt()`.
  * IGVM Builder Integration: Once Stage 2 becomes part of the IGVM builder, validation in Stage 2 might no longer be necessary.
* Lib Module Optimization: The meeting discussed optimizing the Lib module to improve code sharing and build efficiency.

### Other Topcis:

* System Calls Implementation: Peter Fang shared a draft PR for implementing system calls and the device model.
* IGVM with TDX: The meeting discussed the status of IGVM with TDX, which is currently functional but requires code restructuring.


