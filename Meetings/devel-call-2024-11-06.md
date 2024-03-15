# Meeting Minutes: SVSM Development Call (November 6th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Diego Gonzalez Villalobos, Huibo Wang, Joerg Roedel, Jon Lange, Nicolai Stange, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj, Ziqiao ZHou

## Topics:

### Release Process and Naming

* A single release stream with release tags will be used.
* Development releases will be identified by YYYY.MM-devel.
* Stable releases will be identified by YYYY.MM.NN.
* Development releases will not have increasing numbers.
  * Open question: How do do multiple development releases in one month.
* Stable releases will have increasing numbers after the dot.
* A one-week stabilization period will be implemented before development releases.

### Page Invalidation Discussion

* The page invalidation implementation for TDP platforms will be a noop.
* A new platform-independent `delegate` operation will be introduced to handle page delegation to L2.
* The tdx-tdcall crate will be removed and replaced with internal implementations in the COCONUT codebase.
* A dynamic memory carveout mechanism will be implemented for OVMF to support the dynamic memory sizing for SVSM.
  * Needed for allocating a validation bitmap in the SVSM and solve potential double-page-validation attacks.

### Memory Management:

* The team highlighted the need for dynamic memory allocation and stack size optimization to accommodate increasing vCPU counts.
* The impact of large stack sizes, especially in debug builds, was discussed.
* The idea of using dynamic stack expansion was explored as a possible solution.
* The team agreed to investigate ways to reduce stack size in release builds and use tools to identify high stack consumers.

### OVMF IGVM Integration:

* The team discussed the potential for integrating more IGVM functionalities into OVMF, including ACPI tables.
* The initial focus will be on integrating the memory layout information from the SVSM to OVMF.
* The feasibility of integrating other ACPI tables, such as MADT, SRAT, and SLIT, was discussed.

### TLB Shootdown:

* The challenges and potential solutions for TLB shootdown in SMP environments were explored.
* The limitations of current KVM support for inter-L1 interrupts were discussed.
* A short-term solution involving a native platform and IPI-based TLB shootdown was proposed.
* The long-term solution will depend on the progress of KVM's support for multi-privilege levels.

### TPM Reference Code:

* The team discussed the need to migrate to the official TCG TPM reference code.
* Open problem is an additional patch SVSM carries to disable pthreads.
* Solutions will be investigated.

### Setup Verification Code:

* The team will review and provide feedback on the PR for setup verification code.
* The PR will be merged after necessary reviews and CI testing.
