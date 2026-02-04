# Meeting Minutes: SVSM Development Call (February 4th, 2026)

## Topics:

### **TSC Meeting Report & Infrastructure Updates**

* **Stage 2 Rework:** Progress was reported on moving most Stage 2 functions into the IGVM builder to keep Stage 2 minimal; a Pull Request (PR) is currently pending.
* **SVSM Memory Relocation:**
  * Efforts are underway to move the SVSM memory location in QEMU from the 500 GB boundary down to actual guest memory.
  * Jörg proposed a 64MB boundary, but initial tests caused an OVMF panic.
  * OVMF currently struggles with "holes" in lower memory regions as it allocates memory without fully consulting the memory map.
  * Tests at 128MB and 1GB also failed, while 2GB allowed a boot but resulted in a Linux hang.
* **Platform Unification:**
  * The team aims to unify memory addresses across host architectures (Hyper-V, QEMU, and Vanadium).
  * Vanadium currently uses a unique address, but Adam Dunlap confirmed they can move to the unified 64MB range once OVMF issues are resolved.
* **Motivation for Memory Changes:** Moving SVSM into guest memory is a prerequisite for dynamic memory allocation, which is necessary for handling memory state bitmaps on certain platforms.

### **Google Summer of Code (GSoC)**

* The proposal for the "observability" project was updated after feedback indicated the original scope was too large for a 12-week timeline.
* The finalized proposals are now listed on the QEMU GSoC page.

### **Pull Request (PR) Status**

* **Stale PRs:** Discussion focused on PR 719 and 721 regarding multi-key attestation. Adam Dunlap noted that while the work isn't abandoned, it will be picked up in a few months; the current PRs will be closed and replaced with new ones later.
* **Merged PRs:** PRs 920, 922, and 952 have been merged.
* **ACPI Checksum:** Stefano Garzarella raised a question regarding ACPI checksum verification; Jon Lange noted the conversation is ongoing following a comment from Luigi.

### **Technical Discussions**

* **Hyper-V Testing in CI:**
  * Luigi Leonardi inquired about adding Hyper-V checks to the CI to prevent regressions.
  * Jon Lange noted the CI is currently Linux-based and it is uncertain if GitHub's Windows runners support the necessary COCONUT IGVM files yet.
* **VMSA Alignment:**
  * Jörg and Jon discussed a fix regarding VMSA guest-physical alignment.
  * Jon argued against strictly maintaining 2MB virtual-to-physical alignment, as it prevents the use of guard pages on the initial stack without wasting memory.
  * The team agreed to fix alignment-related bugs as they arise rather than forcing strict alignment.
* **TDX Update:** Adam Dunlap informed the group that Google's plans have shifted away from using SVSM in TDX for the time being.
