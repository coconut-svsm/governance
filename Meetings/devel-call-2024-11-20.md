# Meeting Minutes: SVSM Development Call (November 20th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Jon Lange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Build System Transition:

* Joerg Roedel introduced a new build script.
* The script aims to simplify building user space components and the file system image.
* Concerns were raised about potential longer build times and redundancy.
* The team discussed the need for multi-target support in the build script.

### Safe vs. Unsafe Code:

* Jon Lange expressed concerns about the overuse of the `unsafe` keyword.
* The team agreed to align `unsafe` usage with Rust's definition.
* Functions impacting memory layout should be marked `unsafe`; others should not.

### Interrupt Handling Safety:

* Jon Lange raised an issue with interrupt handlers not correctly tracking IRQ state.
* The team agreed to fix this issue.

### AVX and SSE Support:

* Jon Lange proposed making AVX support optional
* The team agreed to implement this change.

### Shadow Stack Setup:

* Jon Lange mentioned an upcoming change to shadow stack setup for better portability.
  * SNP enables shadow stacks in the VMSA - does not work for non-AMD platforms.
  * Change code to enable shadow stacks on AP startup.
* The team agreed on the necessity of this change.
