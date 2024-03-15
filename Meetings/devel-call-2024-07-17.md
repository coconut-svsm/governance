# Meeting Minutes: SVSM Development Call (July 17th, 2024)

## Attendees:

Adam Dunlap, Carlos López, Chuanxiao Dong, Cláudio Carvalho, Derek Miller, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, ramakrishna gali, Roy Hopkins, Stefano Garzarella, Tom Lendacky, Vasant Karasulli

## Topics:

### Updates

* Merges and PRs: Carlos López provided an update on recent merges including TD support, APIC emulation, and bug fixes.
* Io instruction decoding and emulation: Peter Fang's PR is under review and requires additional testing.

### Stage 2 binary size

* Chuanxiao Dong raised concerns about the increasing size of Stage 2 binaries. The team discussed potential workarounds and long-term solutions using IGVM.

### Stack overflow issues

* The team discussed the challenges of detecting and preventing stack overflows in Rust.
* Potential solutions included improving guard page usage, better stack usage tracking, and enhancing the unwinder.

### Default Copy Implementation

* Issue: A lint rule requiring default copy implementations for all structures might be causing unexpected copy operations, leading to increased stack usage and potential bugs.
* Solution: The team decides to remove the lint rule, allowing developers to explicitly implement copy when needed.

### Toolchain Management

* Issue: The current method of using the cargo toolchain might lead to reproducibility issues and potential incompatibility with nightly features.
* Solution: The team will explore using environment variables to specify toolchain versions for different build configurations.

### Virtual Device and VMM Communication

* The primary focus of the discussion was on the need for a communication channel between the COCONUT-SVSM and the VMM to enable feature negotiation and key management. The team explored different approaches to achieve this:
  * Modularization: Introduce a modular system within the COCONUT-SVSM to handle different communication protocols and key management strategies.
  * IGVM: Utilize the IGVM format to pass configuration information and potential communication channels between the SVSM and VMM.
  * Trust and Measurement: Discuss the importance of trust and measurement in the communication channel to ensure security.
* Key Points:
  * There's a need for a flexible communication mechanism between the SVSM and VMM to support various features and use cases.
  * The team leans towards a modular approach to handle different communication protocols and key management strategies.
  * The IGVM format is considered a potential candidate for passing configuration information.
  * Trust and measurement are essential for secure communication, and the team will explore options for achieving this.

### No meeting next week

* Meeting on July 24th is canceled.
* Next meeting on July 31th.
