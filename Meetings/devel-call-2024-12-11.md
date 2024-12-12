# Meeting Minutes: SVSM Development Call (December 11th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, James Bottomley, Joerg Roedel, Kevin Hui, Oliver Steffen, Peter Fang, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### User Mode Allocators

* Joerg Roedel raised the need for a heap allocator in user mode for the SVSM project.
* Several allocator crates were discussed, including embedded-alloc, weealloc, and a buddy-allocator, but each had limitations (fixed heap size, C code dependency, etc.).
* James Bottomley suggested considering the standard library allocator Rust uses, which could be hooked to malloc from musl libc. This approach could offer compatibility with existing Rust programs and potential for future kernel-side integration.
* Joerg Roedel agreed to investigate musl libc integration further.

### VTPM Update

* James Bottomley inquired about the status of vTPM driver work for Linux and OVMF.
* Tom Lendacky informed that Stefano is preparing a V2 submission for the Linux driver with necessary changes.

### SVSM Observability

* Joerg Roedel initiated a discussion on SVSM observability, highlighting the need for guest OS access to runtime parameters (logs, module information, memory usage) without relying on console output.
* Peter Fang suggested using GHCI as a communication channel for Intel platforms, but concerns were raised about host visibility and potential security implications.
* James Bottomley proposed a mechanism involving encrypted memory to bypass the host and communicate directly with the SVSM.
* Joerg Roedel emphasized the desire for a common set of commands for querying observability data across platforms.
* Peter Fang agreed to explore possible implementations on the Intel side.

### VirtIO-Block Driver

* Joerg Roedel and Oliver Steffen discussed the virtio-block driver PR.
* Key points included the need for clear boundaries between safe and unsafe memory and potential improvements to the virtio-block interface.
* The possibility of importing the virtio-block crate into the codebase was considered, with a focus on asynchronous operation support.

### Device Model PR

* Joerg Roedel provided feedback on the device model PR, suggesting prefixing user components with "user" to simplify exclude command lines.
* Vijay Dhanraj acknowledged the feedback and expressed his intention to address it.

### Console PR

* Joerg Roedel mentioned plans to rebase the console PR and merge it quickly.

### Attestation Protocol

* Dionna Glaze raised a question about the binding attestation method, specifically the similarity between single service and all services attestation reports when only one service exists.
* James Bottomley clarified the potential security implications of this similarity.
* It was decided to discuss this further with Tom Lendacky and potentially update the SVSM specification.
