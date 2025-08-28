# Meeting Minutes: SVSM Development Call (August 20th, 2025)

## Topics:

### TSC Call Update:

* **Review of Development Plan Document:**
  * The TSC plans to review the SVSM development plan document over the next few weeks.
  * They will propose which items to keep, remove, and add to ensure the document aligns with the project's direction.
  * The updates will be discussed in PRs and on future calls.

* **OVMF and SVSM Changes for Memory Map Consumption:**
  * Jörg and Jon discussed the progress Peter has made on changes that allow OVMF to consume the IGVM memory map from SVSM.
  * This feature is important for SVSM to allocate a variable amount of guest memory for data structures, such as page validation state bitmaps, whose size is not known at compile time.
  * These validation bitmaps are needed to fix security issues and enable features like live migration and guest reboot.
  * The team needs to decide on a timeline for making this a requirement. Before the changes are upstream, everyone using SVSM will need to use the downstream OVMF.
  * Adam Dunlap said that carrying a couple of downstream patches into their OVMF is probably okay, but it would be annoying if they were in constant flux and hard to manage.
  * Jon Lange offered to share the patches with Adam for a risk assessment on whether they are in good shape for an upstream merge.
  * Richard Relph's current reboot work is tracking page validation calls with a run-length encoded bit structure. He believes it will be easy to switch to a full bitmap system when available. He is close to submitting his first PR for this work, with the main holdup being a discussion on how to handle the GHCB transition. Jon Lange projects that his own PR on using full bitmaps would be submitted after Richard's.

* **MMIO API Discussion (PR775):**
  * The TSC discussed PR775, which introduces MMIO support for the native platform.
  * The current API is problematic because it works on slices and does not guarantee single operations for slice reads and writes.
  * A new API is desired, but will be implemented and submitted separately.
  * Jon Lange noted that the compiler can be relied upon to perform single writes for primitive integer types, and the current code casts the slices to these types to ensure correct volatile operations.
  * He believes the current implementation is correct but not elegant, and it can be submitted as is without being wrong.
  * Jörg asked Jon to add this explanation as a comment to the PR so they can move forward with it.
