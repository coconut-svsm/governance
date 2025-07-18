# Meeting Minutes: SVSM Development Call (July 9th, 2025)

## Topics:

### Opening and Announcements

* Jörg Rödel announced he will be on vacation for the next two weeks.
* Next week's meeting will be led by Jon Lange.
* The following week's meeting will be led by Stefano Garzarella.
* No significant impact on merging is expected as everyone in the TSC has merge rights.

### Zoom Issues and Alternative Conference Software

* James complained about Zoom's dual-monitor behavior and suggested switching to open-source conference software.
* Jörg Rödel is open to alternatives if they support reliable transcriptions and allow multiple people to drive the meeting.
* James proposed BigBlueButton (BBB) if transcriptions can be made to work for LPC. Jörg confirmed BBB could be considered.

### SVSM Specification Updates (Tom Lendacky - AMD)

* Tom Lendacky will release another draft version of the SVSM spec.
* This draft will include changes to the vTPM manifest version, specifically adding a new version that lists all keys, simplifying the process by eliminating the extended single service call.
* He is awaiting feedback from Gerd regarding UEFI service documentation for request and response links.
* He noted that the DB and DBX databases are already measured as part of a PCR, so they don't need to be in the manifest, leading to a more concise manifest.
* Jörg Rödel asked Tom Lendacky to review PR 701 (UEFI protocol number) as he owns the SVSM protocol spec.

### Rust Toolchain and Verification Breakage (Ziqiao Zhou)

* Jörg Rödel brought up Issue 700, which reports a breakage in Verus verification with the new Rust toolchain.
* Ziqiao Zhou confirmed the issue and stated that with recent updates to Verus (supporting versions below 1.88), she will be able to update the Verus version to be compatible with the latest SVSM codebase, fixing the breakage.
* Once fixed and rebased, Ziqiao will rebase PR 679 (verification for the educator) for merging.
* Jörg expressed minor hesitation about annotations making the code harder to read but believes the benefits outweigh this.

### IGVM Series and QEMU Support (Stefano Garzarella - Red Hat)

* Stefano Garzarella announced that the IGVM series has been queued by Paolo and should be landing soon. This is a missing part in QEMU to run SVSM.
* Jörg Rödel and Stefano Garzarella extended thanks to Roy and everyone involved for their efforts in reviewing and pushing maintainers. This is a significant step forward for the next release.

### EDK2 Rebase and Downstream Patches (Oliver Steffen)

* Stefano Garzarella inquired about rebasing the EDK2 branch.
* Oliver Steffen confirmed that a PR has been opened to rebase EDK2. Most changes are upstream.
* Remaining downstream patches are:
  * A workaround to disable the EFI memory attributes protocol for Linux distributions where GRUB hasn't adapted to OVMF changes (convenience for booting Fedora).
  * Setting an EFI variable to bypass the blue screen in Shim when booting with a TPM for the first time (convenience for SVSM where reboots are not possible).
* Jörg Rödel sees no reason to block the rebase, as these are primarily workarounds.
* Oliver Steffen also reminded the team about new patches for MMIO slots for block storage, sent to the QEMU list, and welcomed comments.
* Stefano Garzarella noted he doesn't have merge permissions for EDK2 and will ping Jörg. Jörg will check and fix permissions across repositories.

### Unsafe Block Documentation Effort

* Stefano Garzarella provided an update: The current main branch has around 100 uncommented unsafe blocks. With PRs in flight, the number is closer to 20-30.
* Jörg Rödel stated that with the memory management and partial CPU merge, the number is down to 13.
* The remaining unsafe blocks are likely cases that are genuinely unsafe or require refactoring (e.g., `cpu/vmsa.rs` file).
* Stefano Garzarella suggested opening issues to track the remaining unsafe blocks and find people to work on refactoring them.
* Jörg Rödel thanked everyone for the great effort, noting they started with over 200 unsafe blocks and are now down to a very low number.

### Monthly Development Releases

* Jörg Rödel announced a decision from the TSC meeting to start monthly development releases for SVSM, likely beginning in August.
* This is for workflow and psychological reasons, providing checkpoints for discussions on features and bugs.
* It will allow people to report bugs against specific releases and tie features to particular releases (e.g., "October 2025 release").
* These will be monthly snapshots, not tied to feature integration.
* Before each development release, Jörg plans to conduct more thorough testing, including verification, fuzzing, and testing release builds, exceeding the usual pre-PR merge testing.
