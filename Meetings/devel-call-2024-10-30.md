# Meeting Minutes: SVSM Development Call (October 30th, 2024)

## Attendees:

Chris Hawblitzel, Huibo Wang, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Tom Dohrmann, Tyler Fanelli, Vasant Karasulli, Vijay Dhanraj, Ziqiao Zhou

## Topics:

### Formal Verification Efforts

* Joerg Roedel proposed starting formal verification efforts using Verus tool.
* Tom Dohrmann raised concerns about Verus documentation and suggested improving it for better community adoption.
* Chris Hawblitzel acknowledged the lack of documentation and promised to prioritize it.
* Ziqiao Zhou explained using existing test cases for reference while documentation improves.
* Joerg Roedel emphasized the importance of maintaining annotations for successful verification.
* Ziqiao Zhou proposed minimizing annotations and offering temporary disabling mechanisms.
* Agreement to discuss further on the mailing list and raise potential objections.
* Decision to update the PR with minimal annotations, verification process documentation, and maintainance pointers.

### User Space Testing and Shadow Stacks

* Tom Dohrmann inquired about the status of his Shadow Stack PR.
* Joerg Roedel explained plans to integrate user space testing into the repository and mentioned encountering issues with dynamic binaries.
* Tom Dohrmann offered assistance with cargo and linker issues.

### User Space Enabling PR

* Vijay Dhanraj presented his user space PR split-up plan and received feedback from Joerg Roedel.
* Joerg Roedel agreed on the plan and expects some discussions around init process PRs.

### Virtio-Block PR

* Joerg Roedel asked for update on the Block PR from Oliver Steffen.
* Oliver Steffen explained encountering memory handling issues and limitations with CPU mapping.
* Joerg Roedel suggested temporary workarounds and suggested `SharedBox` for shared memory allocation.
* Oliver Steffen agreed to investigate further and look into `SharedBox`.
* Oliver Steffen also mentioned taking over the vTPM driver work in EDK2 and Linux kernel.

### Stage2/SVSM Split Work

* Tom Dohrmann provided an update on separating stage two and the kernel. He mentioned challenges and proposed separating virtual address types into a common crate.
* A discussion occurred regarding the fuzzing setup and limitations with library usage for dead code removal.
* Agreement to prioritize stage two separation and consider future improvements for the kernel.
* Joerg Roedel suggested potentially splitting components into separate sub-crates for better organization.

### New Release Process

* Joerg Roedel announced plans to draft an initial release process proposal.
* The proposal will include development and production release types.
* The proposal will be sent to the mailing list for discussion before the next meeting.
