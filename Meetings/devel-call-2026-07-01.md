# Meeting Minutes: SVSM Development Call (July 1st, 2026)

## Topics:

### Release Update

* **New Release Available:** Jörg said the new SVSM release was tagged on Monday and is now generally available for testing.

### TSC Meeting Update

* **Fallible Allocation Plans Discussed:** The TSC spent much of its meeting discussing the design and progress of fallible allocations. SVSM currently relies on stable Rust allocation APIs that panic when an allocation cannot be fulfilled, which is undesirable for the project.
* **Configurable Allocators Are Also a Goal:** Jörg said SVSM wants configurable allocators for collections and smart pointers such as `Vec`, `String`, maps, `Box`, `Rc`, and `Arc`.
* **Custom Implementations Required:** Stable Rust does not currently provide all the needed fallible, allocator-aware APIs, so the work requires custom collection and smart-pointer implementations. Carlos has been leading this effort.
* **Common Infrastructure May Serve Other Projects:** Other projects outside COCONUT have similar requirements and would like to build on shared infrastructure. Reusing the Linux implementation is not currently an option, and the TSC discussed the design challenges involved in creating a common solution.
* **Exit Code for Unhandled Exceptions Still Undefined:** The TSC revisited the user-task exit-code PR. It still needs to define an exit code for tasks killed by unhandled exceptions. Linux uses 128 plus the signal number for signal termination, but SVSM has no signals and therefore needs its own convention.

### Page-Table API Safety

* **Walking Inactive Page Tables Is Unsafe:** The TSC followed up on the previous development-call discussion about the page-table crate. The current page-table walking code only works safely for an active page table.
* **Inactive Page-Table Walks Are Not Needed:** The group concluded that SVSM has no need to walk inactive page tables, so the API should make such walks impossible.
* **Walking Logic Should Target the Active Table:** Jörg said the likely design is to move walking code out of the page-table structure and expose functions that always operate on the active page table.

### CI on Intel Hosts

* **KVM Fix Reached Linux 7.2-rc1:** Carlos' fix for the intermittent CI failure on Intel hosts has been merged into Linux 7.2-rc1. The project is waiting for the fix to reach stable kernels and eventually the kernel used by the CI runner.
* **CI Will Continue Using KVM:** The TSC reconsidered switching the affected CI tests from KVM to TCG. Jörg said the failures are not frequent enough to justify the change, so CI will remain on KVM for now.
* **Situation Will Be Monitored:** The decision can be revisited if the failures become a larger problem.
