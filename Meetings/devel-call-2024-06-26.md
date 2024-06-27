# Meeting Minutes: SVSM Development Call (June 26th, 2024)

## Attendees:

Chuanxiao Dong, Cláudio Carvalho, Huibo Wang, James B, Joerg Roedel (Chair), Nicolai Stange, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Announcements

* Joerg Roedel will be away for the first two weeks of July. Next meeting will be on July 17th.
* Roy Hopkins and Carlos Lopez have been nominated to merge PRs during Joerg Roedel's absence.

### SysCall API Discussion

* Unfinished documentation - Needs clarification on underlying object concept and Rust-like object types.
* ABI definition for calling Rust functions - Possible to reuse existing Linux kernel implementation.
* James B suggests following the Linux kernel ABI for consistency.
* Joerg Roedel agrees to look into how Linux does it.

### System Call Implementation in Kernel

* Chuanxiao Dong asks for more detailed documentation on system call implementation in the kernel.
* No detailed document exists yet - Joerg Roedel is still working on it.
* Volunteers welcome to help write the document or prototype an implementation.

### Kernel vs. User Space for MSR Emulation

* Debate on whether MSR emulation should be done in kernel or user space.
* James B suggests a similar approach to KVM, where some MSRs are handled in kernel and others are passed to user space.
* Joerg Roedel agrees a similar approach should be taken for SVSM.

### VMM Object Sharing Between Processes

* Discussion on challenges with sharing VMM objects between processes for device emulation.
* Joerg Roedel clarifies that objects are moved, not copied, when transferred between processes.
* Locking mechanisms will be needed for safe access by multiple threads within the same process.
* Multiple VMM objects cannot be created for the same VM within the same process.

### Memory Mapped Area for Object Data Transfer

* The format for the memory mapped area used for object data transfer between kernel and user space is object specific and not yet defined.
* A simple definition will be established initially and extended as implementation progresses.

### Device Model Process to Inject IRQ Events

* IRQ event injection for device models is discussed.
* Joerg Roedel suggests using an IRQ object similar to Linux eventfd, which can be bound to a specific APIC.
* The actual implementation details depend on the APIC design.

### Rust Standard Library support for COCONUT:

* There is no estimation on the effort required yet.
* Initial focus will be on creating a library that user space can be built against.
* This library will provide a Rust-like API for memory allocation, collections, and channels.
* Additional libraries will be needed for specific SVSM specific functionalities.

### Initial library development:

* The memory allocator is already under development and nearing completion.
* A prototype of the library will be available after Joerg Roedel's vacation.
* Chuanxiao Dong expressed interest in reviewing and contributing to the prototype.

### Early Attestation and Management Architecture:

* Stefano Garzarella is working on a document outlining the architecture.
* A link to the Google Doc will be shared in the meeting chat or mailing list for collaboration.
* A PR will be submitted for further discussion once the document is complete.

### Call for Sessions: Confidential Computing Microconference at PLumbers

* The deadline for submitting session proposals is July 15th.
