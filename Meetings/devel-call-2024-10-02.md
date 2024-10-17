# Meeting Minutes: SVSM Development Call (October 2nd, 2024)

## Attendees:

Adam Dunlap, Christopher Oo, Cláudio Carvalho, Diego Gonzalez Villalobos, James Bottomley, Joerg Roedel, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Platform Abstractions vs. Exception Handling:

* Discussion on whether to use VC/VE exceptions or platform-specific abstractions.
* Decision: Generally use VC/VE exceptions where possible. Use platform abstractions when necessary or needed for performance reasons.

### SVSM Host Kernel Patches:

* Status: Patches are not ready for merging due to missing VMPL support in KVM.
* Next Steps:
  * Roy Hopkins is preparing a 6.11 kernel with necessary downstream patches.
  * Tom Lendacky shared a link to the KVM community call for further discussions.
* SVSM downstream kernel will unblock SVSM IRQ work and make it independent from KVM upstream progress.

### Other Announcements:

* Next Meeting: The next meeting will be in two weeks due to Joerg Roedel's vacation.
