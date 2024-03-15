# Meeting Minutes: SVSM Development Call (May 22th, 2024)

## Attendees:

Adam Dunlap, Carlos López, Cláudio Carvalho, Derek Miller, Dionna Glaze, Harvey Danger (us-kir-6tha), Huibo Wang, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Ramakrishna Gali, Roy Hopkins, Stefano Garzarella, Thomas Leroy, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj, Zhaorong Hou

## Topics:


### Panic Strings and Memory Footprint

* Jon Lange raised a concern about the potential size of panic strings in the binary and the impact on memory footprint.
* He suggested exploring ways to reduce the size of panic strings, such as using shorter messages or error codes.
* Joerg Roedel suggested removing debug messages from production builds.
* Carlos López suggested using minimum logging levels and exploring alternatives to panic strings like unwrapping errors.
* It was agreed to measure the size of the string section to understand the impact of panic strings.

### Validation Bitmaps and Memory Consumption

* Jon Lange discussed the need for dynamic memory allocation for validation bitmaps in the SVSM.
* Current limitations in QEMU and OVMF prevent placing the SVSM in the middle of guest memory.
* Jon Lange proposed using a protocol to communicate the memory map from the hypervisor to the SVSM.
* Peter Fang suggested using IGVM format for memory map communication.
* Jon Lange and Peter Fang agreed to collaborate on changes to the COCONUT codebase and OVMF to implement this solution.
* Tom Lendacky requested more information about the proposed approaches for parameter consumption in OVMF.
* The group decided to prioritize a cross-platform solution for parameter consumption.

### Task Assignments and Development Plan

* Peter Fang requested clarification on task assignments in the development plan, as the project is rapidly growing.
* Joerg Roedel suggested using the development plan document on the public [GitHub documentation page](https://coconut-svsm.github.io/svsm/developer/DEVELOPMENT-PLAN/) and having people update it with their assigned tasks. This can be done through pull requests (PRs).
* Carlos López discussed the plan for implementing "fallible allocations" using a fork of the upstream Rust allocator. He explained the need for separate approaches for basic abstractions and higher-level smart pointers.
* Joerg Roedel mentioned future plans to make bigger changes to the allocator infrastructure in the kernel using the same heap allocator being built for user space. This will involve changes to the page allocator and eliminating the need for direct memory mapping.
* The group agreed that people working on specific tasks should submit PRs to update the development plan document to reflect their assignments.

### User Space Design

* Peter Fang mentioned the PR submitted for discussion on the user space interface.
* Joerg Roedel acknowledged the PR and expressed interest in a more detailed discussion after reviewing it.
* Peter Fang highlighted their interest in exploring an event system for communication, as an alternative to the traditional system call approach proposed in the PR. He also offered to provide a PDF version of the user space design document.
* Jon Lange requested a PDF version of the user space design document for easier review.
