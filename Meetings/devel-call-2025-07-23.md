# Meeting Minutes: SVSM Development Call (July 23rd, 2025)

## Topics:

### Persistent Storage File System - Cocoon FS Presentation

* Presenter: Nicolai Stange
* Topic: Discussion about the file system format for SVSM persistence, designed to go on top of the VirtIO block implementation.
* [Slides](Data/cocoonfs-svsm-devel-pres.pdf).
* Cocoon FS Overview:
  * Designed specifically for TEEs (Trusted Execution Environments).
  * Every entity is encrypted with a fresh initialization vector.
  * Whole file system image authenticated by a Merkle tree, where a single digest captures the entire state.
  * Supports any algorithm defined by TCG (Trusted Computing Group) for cipher and hash.
  * Includes a journal.
  * File names are numbers (inode numbers).
* Discussion Points:
  * Comparison to existing solutions: James questioned why a new file system was invented instead of using standard solutions like EroFS + Fs-crypt.
  * Nicolai clarified that EroFS is read-only, and the main challenge for Cocoon FS was integrating a journal with Merkle tree authentication.
  * Partial File Writes: Not possible with Cocoon FS as files are encrypted as a whole. This is acceptable for TCG TPM states which write out the state entirely.
  * Rust Implementation:
    * Follows best practices (e.g., no allocation failures).
    * Uses the Cocoon TPM crypto abstraction.
    * Generic over locking and block storage interface.
    * Transaction-based (all or nothing).
    * API defined using Rust's async/future framework.
  * Rust async/future discussion:
    * James inquired if it was "yet another Async framework." Nicolai explained it's a single trait defining the interface for asynchronous operations, similar to promises in JavaScript.
    * Concern raised by James about the "polling" mechanism, suggesting it could be inefficient compared to event-driven models. Nicolai clarified that the poll method is invoked by an executor (environment), which can either busy-poll or wait for interrupts, making it execution environment agnostic.
* Next Steps (Cocoon FS):
  * Nicolai will implement the block interface trait on top of the VirtIO block implementation.
  * This will allow Cocoon FS to be used for storing TPM state.
  * Action Item: Stefano suggested making it optional (e.g., a feature flag) for future flexibility and to allow for other file systems. He looks forward to reviewing the Pull Request (PR).
   * Offline vs. Online Manufacturing: Nicolai asked if the file system should be formatted and TPM state manufactured on the first boot or offline.
   * Stefano suggested starting incrementally with online manufacturing, but agreed that offline manufacturing tools would be beneficial in the long term.
   * Nicolai noted that an offline tool to format and store a single file would be quick to implement.

### Undocumented Unsafe Blocks
* Stefano Garzarella reported that all undocumented unsafe blocks appear to have been documented.
* Some PRs are still in flight for review.
* A PR was sent to enable the Clippy linter on these unmerged PRs, and everything seems fine, indicating successful documentation.

### KVM Forum Attendance
* Discussion: Stefano asked if anyone would be joining the KVM Forum to potentially organize a gathering.
* Attendees Confirmed: Stefano, Oliver, and Luigi will be attending.
