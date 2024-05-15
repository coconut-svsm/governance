# Meeting Minutes: SVSM Development Call (May 8th, 2024)

## Attendees:

Chuanxiao Dong, Cláudio Carvalho, Eddie Dong, Elena Reshetova, Harvey Danger, Huibo Wang, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Sathya Narayanan, Stefano Garzarella, Tom Lendacky, Vijay dhanraj, Wei W Wang

## Topics:

### Announcements

* The SVSM project fully onboarded to the Confidential Computing Consortium.
* Joerg Roedel will share a development plan document later this week. Everyone is encouraged to read it so the community can discuss it in the next meeting.

### SVSM-on-TDX Architecture Discussion (IRQ part)

* Joerg Roedel presented the initial plan for TDX support, which involves bringing basic TD support and creating platform abstractions to eliminate AMD SEV-SNP assumptions from the code.
* Jon Lange discussed his ongoing work on emulating the APIC for interrupt management, emphasizing the need for a cross-platform approach to get alignment between SNP and TDX. Interrupt source registration is crucial for both platforms.
* Joerg Roedel clarified that main criteria for merging TDX code is that it not breaks other platforms. The design does not need to be perfect and can be improved later. There was agreement that communication interfaces between hypervisor, SVSM, and guest OS need more care and thought up-front.
* There was debate on the ideal approach for interrupt delivery, with Jon Lange advocating for a method using a shared page and bit manipulation instead of ring buffers. Eddie Dong suggested industry standardization for the interface.
* A decision was made to distribute Jon Lange's proposal on interrupt management interfaces more broadly within the community after incorporating feedback from Intel and AMD.
* The need for collaboration on timer support within the SVSM was identified. Jon Lange suggested that timers could be handled as regular interrupts, with additional logic potentially implemented later.
* **AI**: Jon Lange will finalize the APIC emulation code and submit it for review, with a focus on interrupt injection for now.
* **AI**: The document outlining the proposal for interrupt management interfaces will be shared with a wider audience after incorporating feedback from Intel and AMD.
* **AI**:Further discussion is needed to determine the best approach for timer support within the SVSM.

### SVSM-on-TDX Architecture Discussion (Platform Abstraction Part)

* Jon Lange suggested two approaches for platform abstractions:
  1. Develop a full abstraction layer first, potentially delaying TDX implementation.
  2. Focus on TDX-specific abstractions for a quicker start.
* Jon Lange asked about TD booting for SVSM and the use of a trampoline page
* Peter Fang will consider revising his trampoline page implementation to:
  * Allow launching guest VCPUs from different EIPs.
  * Start in 32-bit mode for while transitioning to 64-bit mode on the trampoline page.
  * Explore starting firmware outside the reset vector.
