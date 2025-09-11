# Meeting Minutes: SVSM Development Call (September 10th, 2025)

## Topics:

### TSC Meeting Update

* Discussed upcoming September release and pending PRs.
* All targeted PRs have been merged → release on track.
* Planned release in calendar week 39 (two weeks).
* Ongoing discussion on handling AI contributions; no conclusion yet, to be revisited.
* Update from KVM Forum shared by Stefano.

### KVM Forum Update

* Talks on SVSM:
  * Stefano & Oliver: status update since last year; persistent storage progress.
  * Discussion on new services: secure TLS channel for logs/memory dumps; interest from Linaro.
  * SVSM bus in Linux to auto-discover devices; debate on using VirtIO vs. dedicated bus.
  * Concerns raised: VirtIO is guest-host, SVSM is guest-internal → conflicts with multiple buses and platform portability.
* Other SVSM-related talks:
  * Vaishali: reliable timekeeping & trusted clock alternatives.
  * Tobin: attesting confidential devices (high-level tooling).
* Gerd: UEFI variable services related to SVSM.
* David (AMD): SEV firmware update.
* Other highlights:
  * Rust adoption in QEMU (RAS support).
  * Discussion with Pangaj Gupta on live migration; PoC expected.
  * TDX support: acknowledged ongoing work, but no timeline.

### Spell Checker in CI

* Proposal: introduce spell checker into CI to reduce typos.
* Discussion points:
  * Risk of false positives (locale variants, e.g., “color” vs. “colour”).
  * Consensus: too disruptive in CI → better for optional/pre-commit hooks or standalone scripts.
* Suggestion: integrate into Git hooks (non-blocking) rather than CI pipeline.
* Agreement: explore lightweight pre-commit or script-based approach.

### Planes Work

* Current plan:
  * Add device plane awareness in QEMU.
  * Implemented device-plane machine property for IRQ assignment.
* Per-device overrides possible.
* Devices can be listed in ACPI tables or Device Tree for SVSM consumption.
* Enables SVSM to detect runtime-assigned devices and their intended roles (console, attestation, debug, etc.).
