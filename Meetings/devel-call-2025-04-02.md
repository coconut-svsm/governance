# Meeting Minutes: SVSM Development Call (April 2nd, 2025)

## Attendees:

Adam Dunlap, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, John Allen, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tom Lendacky, Vaishali Hasmukhlal Thakkar, Vasant Karasulli

## Topics:

### Stack Issue Investigation:

* Joerg investigated a stack issue and found high stack usage in the page table code.
* Stefano mentioned key generation for attestation might be a factor.
* Joerg shared a script to check stack sizes.
* Stefano will work with Tyler to investigate further.

### TPM Service and Attestation:

* Dionna discussed adding a new call to the ATTEST protocol to allow attesting more than one endorsement key.
* A manifest selector was proposed to provide a key template for TPM.
* James Bottomley and Tom Lendacky provided feedback and discussed the implementation details.
* Issues related to long-running calculations and potential delays were raised.
* The single-threaded request-response model of SVSM was discussed as a potential bottleneck.

### SVSM and Preemption:

* Discussion on preemption within SVSM, especially with long-running calculations.
* Concerns about potential guest kernel panics due to delays.
* Possible solutions like a "busy" return code or multi-threading the call were discussed.
* The need for careful handling of interrupts within SVSM was highlighted.

### Guest Memory Access:

* Dionna discussed the safety of read and write interfaces to guest memory.
* Joerg confirmed that the memory map covers the entire SVSM memory region.
* Discussion on handling exceptions for guest pointers and user pointers.
* The need to check for VC exceptions in user mode was identified.

### Copyright and Author Attribution:

* Dionna raised the question of author attribution and copyright notices in files.
* The practice of putting individual author names was discussed, along with using a generic term like "SVSM authors."
* Multiple copyright lines from different companies were deemed acceptable.
