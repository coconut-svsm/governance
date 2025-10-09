# Meeting Minutes: SVSM Development Call (September 24th, 2025)

## Topics:

### Technical Issue: `slab` Crate Dependency

* Jörg Rödel inquired whether the `slab` crate was a direct or indirect dependency.
* Luigi Leonardi confirmed it is an indirect dependency.
* The dependency comes from the `aproxy` crate.
* It is used in the user space part of the project, not the kernel.

### Technical Issue: Runtime Assertion and Binary Size Limitation

* Oliver Steffen reported a issue where adding one line of code caused a runtime assert (launch error), suggesting a potential binary size limitation.
* The runtime assert is in `page_table.rs` (line 1246) and checks that the region start is not aligned with a huge page.
* Luigi suggested using `git blame` to find the original commit that introduced the assertion.
* Jörg Rödel questioned the validity of the assert, stating a 4K mapped region can still be aligned to a huge page size.

### September Development Release

* Jörg Rödel announced that the September development release was tagged and is out.
* He encountered issues with GitHub preventing the direct push of the commit/tag.
* The "shortcut" used to complete the push was temporarily disabling branch protection for about five minutes.
* Stefano Garzarella proposed the Rust VMM practice as a long-term workaround: open a Pull Request (PR) to prepare the release, merge the PR (using rebase to avoid a merge commit), and then push the tag.

### TSC Meeting Summary

* The Technical Steering Committee (TSC) discussed several Pull Requests (PRs), including those from John and Richard.
* Progress on a large **CocoonFS** was limited due to its size.
* This led to an ongoing discussion in the TSC on how to approach big changes (which will be brought back to this call once the TSC has a proposal).
* The TSC also briefly discussed the **AI code submission issue**, which is also inconclusive and will be revisited in this call later.

### QEMU/IGVM Update and VGA/GPU Issue

* Stefano announced that the QEMU was updated to rebase on QEMU 10.1.
* The `svsm-igvm` branch now points to this update.
* Vaishali confirmed the VGA issue is being tracked separately, but a related issue concerning GPU passthrough (specifically with the H100 card and `VGA none`) has been reported by users after the QEMU update.
* Vaishali does not currently have a testing setup for the H100 card and needs further clarification from the reporters.
* Jörg noted that additional patches might be required for device passthrough, as upstream QEMU may not yet support configuring VMs for this use case.

### LPC Attendance and BoF

* Jörg Rödel submitted a **"COCONUT-SVSM BoF** to the **Linux Plumbers Conference** and hopes for a one-and-a-half-hour discussion slot.
* Stefano asked about remote attendance.
* James confirmed the conference will be **hybrid (virtual)**.
* For a longer BOF slot (suggested time), the BOF will likely be in a non-AV room, requiring the BOF runner (Jörg) to manually set up all AV equipment (e.g., connecting a laptop to a speaker/mic provided by the conference).
* The time difference between Japan (the location) and Europe is approximately 8 hours.

