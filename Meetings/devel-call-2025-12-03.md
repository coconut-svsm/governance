# Meeting Minutes: SVSM Development Call (December 3rd, 2025)

## Topics:

### **TSC Updates**

* **Merge Process:** The Technical Steering Committee (TSC) decided to implement a default 24-hour waiting period before merging pull requests to allow members in different time zones time to review.
* **Roadmap:** Discussions regarding the project roadmap have been deferred until after the Linux Plumbers Conference to gather additional input.
* **Release Schedule:** A December development release is planned for two weeks from now, before the holiday break.

### **Linux Plumbers Conference (LPC) Planning**

* **Scheduling:** The SVSM Birds of a Feather (BOF) session has been scheduled for Saturday, December 13th.
* **Conflict Resolution:** Jon Lange noted a schedule conflict between the Coconut BOF and the x86 microconference.
* **Remote Access:** The BOF is currently assigned to an AV-equipped room, which will facilitate remote participation. If AV is unavailable, Jörg Rödel will set up a laptop to stream audio for remote attendees.
* **Attendance:** Several team members, including Jörg Rödel, Luigi Leonardi, and Stefano Garzarella, plan to attend FOSDEM as well.

### **Technical Discussions**

* **Debug Swap & OVMF Issues:**
    * Jon Lange raised an issue regarding a PR failing due to the SEV `debug_swap` feature, where SVSM boots but OVMF subsequently fails.
    * There was a debate on the necessity of `igvmmeasure` consistency checks if the startup state is fully consumed from the IGVM file.
    * Jon hypothesized that OVMF might be attempting GHCB calls for debug registers which fail when virtualization is enabled.
    * **Action Item:** Jon Lange will update his PR to strip the `debug_swap` bit for VMPL2 (maintaining legacy behavior) and update `IGVM measure` to disable the `debug_swap` check.
* **Verification & Allocator:**
    * Ziqiaozhou (Chico) reported working on verification updates due to fundamental changes in the allocator, specifically regarding the low page indicator and metadata pointers.
    * A bug was identified where page number checks were performed against zero instead of `no_page`; this fix will be split into a separate PR.
* **Google Private Preview:**
    * Adam Dunlap announced that Google is launching a private preview of their SVSM feature (using Coconut) and provided a sign-up form for interested testers.
* **Coconut Alloc Issue:**
    * Luigi Leonardi reported that a student from the University of Pisa found a one-line issue in the `coconut-alloc` crate and opened a PR, which Jörg agreed to review.

### **Next Meeting**

* The meeting scheduled for next week is canceled due to Linux Plumbers; the next call will occur in two weeks.

