# Meeting Minutes: SVSM Development Call (November 18th, 2026)

## Topics:

### TSC Meeting Update

* **Stefano Hosted the Call:** Stefano Garzarella hosted in Jörg's absence.
* **No TSC Updates Were Available:** The TSC did not meet this week or the previous week, with KVM Forum travel contributing to the disruption. Stefano had no TSC updates or submitted agenda topics and opened the floor for discussion.

### Rust Toolchain and Firmware Variable-Store Update

* **A Dependency Update Requires a Newer Rust Toolchain:** Luigi explained that a new release of the firmware variable-store crate fixes a shim bug involving the no-reboot variable. The release pulls in a dependency that requires a newer Rust version, so he asked whether there were objections to raising the toolchain version.
* **Participants Had No Objections to a PR:** Stefano encouraged Luigi to open a PR explaining the reason for the update. Adam agreed to the bump, and Nicolai expected it to be acceptable from SUSE's perspective, while suggesting that Carlos could also comment on the PR. Luigi confirmed that Fedora's Rust version would not be an obstacle.
* **Clippy Adjustments Are Expected to Be Mechanical:** Luigi already has a draft ready and said the newer toolchain requires a few small changes for Clippy, including adjustments to nested conditionals.
* **The Fix and Toolchain Bump Should Share One PR:** Stefano requested that Luigi submit the crate update and toolchain bump together, in separate commits. Luigi agreed to do so.

### PR Review Follow-Up

* **Nicolai Will Revisit Luigi's PR:** Before the formal start of the call, Luigi reminded Nicolai that he had questions awaiting review on his PR. Nicolai said he would look at it, hopefully during the week.
