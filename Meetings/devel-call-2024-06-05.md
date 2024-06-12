# Meeting Minutes: SVSM Development Call (June 5th, 2024)

## Attendees:

Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel (Chair), Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Introduction

* Joerg Roedel was out sick last week and did not make progress on the syscall document. He will have it ready early next week.
* Joerg Roedel will be on vacation for the first two weeks of July. There will be no meeting during that time.

### Upstreaming work on dependencies

* Oliver Steffen inquired about the status of upstreaming work on EDK2 and IGVM support for QEMU.
* Roy Hopkins provided an update on the QEMU work. He is waiting on some dependencies to be merged before submitting a patch series.
* Tom Lendacky confirmed that the EDK2 SVSM support patches have been merged for about a month.
* Upstreaming the TPM driver for EDK2 is handled by Cláudio Carvalho

### Persistent storage

* Oliver Steffen opened a pull request for the virtio drivers to provide a block device.
* Discussion centered around how to handle encryption, file systems, and security.
* Jon Lange argued for a standard block storage interface to avoid code duplication for different hypervisors.
* Joerg Roedel voted for using hypervisor-specific interfaces
* Discussion around security of virtio driver code
  * Joerg Roedel suggested forking the virtio code and reviewing it internally to ensure security before merging.
  * Fuzzer for virtio code also needed in the future.
  * Dionna Glaze suggested using a secure supply chain build process to manage dependencies.

### Key distribution for persistent storage

* The current plan is to use a hypervisor provided channel (likely serial) to provide a key for persistent storage during attestation.

### CI system

* Peter Fang proposed incorporating a CI system (like Jenkins) for automated testing.
* Joerg Roedel confirmed there have been discussions about this in the past.
* The challenge is securing funding for resources (machines) to host the CI system.
* Peter Fang will submit a pull request to add this to the development plan.
