# Meeting Minutes: SVSM Development Call (April 10th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Ernestine Anderson, Huibo Wang, Jacob Xu, James Bottomley, Joerg Roedel, Malus Domestica, Nicolai Stange, Oliver Steffen, Roy Hopkins, Thomas Leroy, Tom Lendacky, Vasant Karasulli, Vijay dhanraj

## Topics:

### Discussion on SVSMs role in mitigating [Ahoi](https://ahoi-attacks.github.io/)-Attacks against SEV-SNP:

* Adam Dunlap inquired about plans to use SVSM to mitigate Ahoi attacks
* Requires the SVSM running with restricted injection and injecting IRQs to OS via alternate injection
  * Also some amount of APIC emulation required in SVSM
* Joerg Roedel presented the challenges of implementing VMPLs (Virtual Machine Privilege Levels) in the KVM hypervisor
  * There are three technologies which would benefit from a common interface: VSM, VMPLs, and TDX-Partitioning
  * Current proposal for implementing VSM not ideal for VMPLs and might not work at all for TDX-Partitioning
  * Need to engage with KVM maintainers on a better solution
* Current prototype implementation of VMPLs in KVM uses single IRQ source for all VMPLs
* Other hypervisors implement one source per VMPL
* Need to be resolved for KVM before SVSM can make progress on this
* Joerg Roedel mentioned that restricted injection will be required for SVSM to mitigate vulnerabilities.

### Merging TDX Changes into Linux and QEMU repositories:

* Vijay dhanraj proposed merging his changes related to TDX partitioning with the COCONUT Linux and QEMU code-base.
* Joerg Roedel agreed to merge it into a separate branch until SVSM gets TDX support.
* Joerg Roedel will test changes on SEV-SNP.

### User Space Support Code for SVSM:

* Joerg Roedel provided an update on his progress in developing user space support code modules for the SVSM.
  * Currently working on user-space memory allocator

### Microsoft TPM Implementation:
* Joerg Roedel discussed the decision to maintain a separate repository for the Microsoft TPM implementation due to the challenges of upstreaming changes to the MSTPM library.

### Memory Fault Issue:
* Cláudio Carvalho brought up a recently reported memory fault issue and Roy Hopkins volunteered to investigate it.

### Microsoft TPM debug flags:
* Cláudio Carvalho addressed challenges encountered when using different optimization flags for the Microsoft TPM code in debug and release builds.
* Joerg Roedel suggested enabling SSE instructions in the Coconut SVSM as a sustainable solution.
* Cláudio Carvalho will open an issue to track progress on this

### Next Meeting:
* The next development call will be held in two weeks.
