# Meeting Minutes: SVSM Development Call (February 18th, 2026)

## Topics:

### Administrative Updates

* **Technical Steering Committee (TSC):**
  * Stefano reported that the TSC meeting was skipped this week due to the absence of Joerg and Jon; consequently, there are no new updates from the committee.
* **Meeting Leadership:** Stefano Garzarella filled in to lead the call in Joerg's absence.

### Toolchain and Code Quality

* **Toolchain Upgrade:** Stefano opened a Pull Request (PR) to move the toolchain to version 1.88.
* **Clippy Linting:** The upgrade enabled several new Clippy lints, leading to various code fixes.
* **Bug Discovery:** The new Clippy lints successfully identified one instance of undefined behavior in the codebase.

### Project & PR Updates

* **Launch Script Cleanup:** Luigi Leonardi opened a PR to drop support for old QEMU in the launch script as part of a general cleanup.
* **QEMU Fork Maintenance:** Stefano noted several open PRs in the project's QEMU fork and suggested the team review them.
* **Planes Branch Synchronization:** Carlos López submitted a PR to the `planes` branch to cherry-pick missing commits from the regular SVSM branch. This ensures the `planes` branch supports self-tests and other features available in the main branch.

### Technical Discussion: "Planes" Stability

* **Boot Issues:** Carlos reported that while attempting to boot Linux via EDK2 using the `planes` branch, the system freezes immediately after the GRUB stage.
* **Testing Failures:** Luigi mentioned that Oliver also attempted to boot the `planes` branch without success.
* **Upcoming Refactor:** Joerg is reportedly working on a new version of the "planes" patch set, which will be rebased on top of kernel version 6.19.
* **Regression Concerns:** Carlos noted it is strange that the branch is currently failing, as it was previously functional, raising questions about changes in the test environment.

