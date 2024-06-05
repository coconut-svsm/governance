# Meeting Minutes: SVSM Development Call (May 29th, 2024)

## Attendees:

Adam Dunlap, Carlos López, Chuanxiao Dong, Cláudio Carvalho, Elena Reshetova, Huibo Wang, Joerg Roedel (Meeting Lead), Nicolai Stange, Oliver Steffen, Peter Fang, Ramakrishna Gali, Roy Hopkins, Thomas Leroy, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj, Zhao Rong Hou

## Topics:

### System Call Interface Update:

* Joerg Roedel presented his update on the interface proposal for system call interface. He outlined a new approach that deviates from the event system and utilizes system call classes as the building block.
* For VM interface this approach leverages predefined VM contexts due to hardware limitations.
* Chuanxiao Dong inquired about potential conflicts with the standard Rust library due to the proposed use of numerous syscalls. Joerg Roedel clarified that the VM interface is specific and shouldn't affect the standard library.
* The overall design aligns with Chuanxiao Dong's proposal, with the main difference being the core concept of the COCONUT kernel not following the "everything is a file" concept.
* Joerg Roedel expects to share a more complete document soon

### Updating Dependencies:

* Oliver Steffen brought up the topic of updating dependency crates, like IGVM.
* Joerg Roedel confirmed there are no objections to updating these.
* Oliver Steffen also inquired about updating EDK2 to leverage the latest upstream version with SNP stuff. Joerg Roedel was unsure of the current state of upstream integration but suggested Oliver Steffen investigate and attempt a rebase if possible.

### Updated EDK2 for TDX Booting:

* Peter Fang discussed his plan to submit patches based on a current EDK2 version to enable building the L2 guest in TD partitioning. He expressed concerns about impacting other builds.
* Joerg Roedel confirmed Peters suggestion of creating a separate branch for EDK2 to manage the TDX partitioning approach.
* They also explored alternative solutions like building an OVMF binary that skips the initial early boot process and launches directly from a later stage.
