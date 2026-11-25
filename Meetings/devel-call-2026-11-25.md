# Meeting Minutes: SVSM Development Call (November 25th, 2026)

## Topics:

### TSC Meeting Update and November Release

* **The November Development Release Is Available:** Jörg reported that the TSC had mostly reviewed PRs and assessed their state. The November development release, discussed at the TSC meeting the previous day, is now out. Contributors can fetch and test it and rebase their work on it.

### Rust Toolchain Update and Compiler-Version Policy

* **The Proposed Toolchain Bump Needs Downstream Coordination:** Following last week's discussion, Jörg said the proposed move from Rust 1.88 to 1.91 needs to be checked with downstream users before proceeding. He plans to announce the topic in the next meeting invitation so more stakeholders can attend and give their views. No compiler-version change was agreed during the call.
* **Compiler Upgrades Should Have a Concrete Justification:** James argued that raising the minimum compiler version should require a language feature or another compelling need, to avoid blocking distributions that cannot provide the newer compiler. Jörg explained that a dependency update is driving the current proposal. James cautioned against moving beyond the required version without a reason.
* **Written Guidance Is Needed:** Jörg would like a policy for deciding when new Rust features justify a compiler update. James suggested a conservative starting point, while acknowledging that Rust's evolution may require more flexibility than the Linux kernel's C compiler policy. James will post the kernel's policy to the mailing list as a basis for discussion, with Jörg following up on how it could be adapted for COCONUT.
* **Security Fixes May Force Compiler Updates:** Luigi asked how the project would handle a dependency security fix that requires a newer Rust compiler. James said an unavoidable requirement could justify an upgrade even under a conservative policy. Jörg noted that the same problem will arise when the project maintains stable branches. The policy discussion will continue on the mailing list.
* **Distribution Build Environments Need to Be Considered:** James asked the Red Hat participants to investigate how their distributions would handle similar Rust dependency updates, including whether they would maintain older dependency branches and backport fixes or require upgrades. Luigi did not have a definite answer. Jörg emphasized that the relevant constraint is which compiler versions are available in distribution build environments, rather than just the default compiler shipped to users.

### Page Validation Tracking

* **Future Guests Will Need SVSM to Track Validation State:** The TSC revisited whether page validation tracking is still needed while discussing a pending preparatory PR. Earlier security issues that had motivated the work were mitigated differently, so there is no strong immediate need for a validation bitmap. Future workloads whose guests do not track memory validation state themselves will require SVSM to do so.
* **Implementation Is Expected to Proceed:** Jörg said the preparatory PR itself is fine and that the project will probably move forward with page validation tracking because it will be needed for those future workloads.

### Generic Bitmap Implementation

* **PR 1217 Needs Further Discussion:** The TSC discussed PR 1217, which makes the bitmap implementation more generic. Its current use is mainly the per-CPU allocation bitmap, but planned per-CPU changes will remove the need for that bitmap. The discussion will resume when Carlos returns to determine whether the generic implementation is still justified or a simpler approach would suffice.
