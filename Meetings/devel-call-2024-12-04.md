# Meeting Minutes: SVSM Development Call (December 4th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Huibo Wang, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Thomas Leroy, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj, Ziqiao Zhou

## Topics:

### SVSM Physical Memory Layout and Allocation:

* SVSM reserves a static physical memory region for kernel, user space, and SVSM.
* Naming scheme for physical memory regions should be clarified.
* Initial memory allocation is static, but SVSM can request more from the host OS when SVSM core protocol is in use.
* Dynamic memory demand from SVSM is not anticipated.

### Undocumented Unsafe Blocks:

* Over 200 undocumented unsafe blocks exist.
* Plan to reduce unsafe blocks to zero
* Group blocks by file/subsystem and create issues on GitHub
* Possibly tagging code owners.

### Memory Verification and Casting:

* Casting integers to raw pointers and vice versa can cause issues for verification tools.
* New interface for raw pointers is proposed to track provenance and ensure proper usage.

### Virtio-Blk and Other VirtIO Drivers:

* Progress on VirtIO-Blk and VirtIO drivers, including use of global memory mapping functions and block layer trait.
* Potential for adding VSOCK support.

### Fixed String Replacement:

* Proposed replacing `FixedString` structure with `String` structure from `core::alloc` crate for better Unicode support and reduced memory overhead.
* Unicode support in SVSM is questioned.
* It was confirmed that `FixedString` can be replaced with `String`.

### File-System Calls and Buffer Trait:

* New PR pending which implements File System SysCalls.
* Currently mostly untested.
* Implements new `Buffer` trait to avoid double copying of data.

### OC3 Conference Submission:

* Approaching submission deadline for OC3 conference.
* Discuss potential topics for submissions, including confidential VMs and attestation proxies.

### IGVM Metadata and Reference Values:

* Possibility of adding metadata to IGVM file, such as security version number and signature.
* Plan to include MRTD in IGVM file and investigate standardizing the format.
