# Meeting Minutes: SVSM Development Call (February 5th, 2025)

## Attendees:

Adam Dunlap, Dionna Glaze, Geoffrey Ndu, Joerg Roedel, Liam Merwick, Peter Fang, Tom Lendacky, Vasant Karasulli

## Topics:

### Using OpTEE

* Dionna Glaze proposed defining SVSM as a PE device on Linux to share memory
  and using the OpTEE protocol for late-loading of TPM state.
* Joerg Roedel plans looking into the protocol for the guest OS to talk to the SVSM.
* Joerg Roedel and Geoffrey Ndu will look into the protocol and discuss it next week.

### AMDTEE Driver

* Tom Lendacky responded to a question in the chat about the AMD-TEE driver.

### COCONUT-SVSM Logo

* Dionna Glaze provided an update on the logo, which is still waiting on Linux Foundation legal.

### User-Space Work and Heap Allocator

* Joerg Roedel gave an update on his next work items for user-space support
  * First is getting heap allocator up and running, `coconut-alloc` crate is base.
  * Second step is support for growable stacks.
  * Third step is enhancing task model to support threads and data passing, including exit-codes.
* Peter Fang will remove the external body allocator from the feature PR.
