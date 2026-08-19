# Meeting Minutes: SVSM Development Call (August 12th, 2026)

## Topics:

### TSC Meeting Update

* **Page-Table Redesign Discussed:** The TSC spent much of its meeting outlining the future of the page-table code. The code will remain within SVSM rather than being factored into a generic crate because significant changes are planned and the project does not want to maintain API stability yet.
* **Direct-Map Dependency Should Be Removed:** The current page-table code relies heavily on SVSM's direct map, which is intended to go away. The redesigned code should instead make greater use of the existing self-map.
* **Lifetime and Ownership Handling Needs Improvement:** The redesign should better manage the lifetimes of page tables and their components, clarify who owns the ability to modify them, and improve locking.
* **Shared Page-Table Paths Expose a Locking Bug:** Jörg said locks are currently associated with individual page tables even though different page tables can share paths. This is safe under current usage but must be fixed for future use, including user space.
* **High-Level Design Document Planned:** The group will create a high-level design document, continue the discussion around it, and then implement the redesign and update users of the page-table code.
* **CocoonFS Merge Completed:** Jörg announced that the CocoonFS work had merged and thanked everyone involved.
* **TPM Integration Is the Next Persistence Step:** Stefano is working on connecting persistence to the TPM.
* **Device-Tree Integration Should Make Persistence Optional:** Further device-tree work should allow persistence dependencies to be configured at runtime and compile time. A persistence-enabled SVSM currently panics if expected services such as the KBS or attestation proxy are unavailable.
* **`ready-to-merge` Label Meaning Clarified:** Once one TSC member has reviewed and approved a PR, that member can apply the `ready-to-merge` label. Other TSC members can still review it, but the label now indicates that the required TSC approval has been given.
* **CAA Alignment Requirement Needs Investigation:** The TSC discussed PR 1186, which enforces the SVSM specification's 4 KiB alignment requirement for CAA regions. The reason for that requirement in the specification remains to be investigated.

### Contribution Guidelines

* **Contribution Guidelines Update Opened:** Jörg opened PR 1192 to refresh `CONTRIBUTING.md` and document expectations that were already applied in practice.
* **Clippy Requirement Documented:** The update explicitly states that contributions must be clean under Clippy, matching an existing CI requirement.
* **Commit Series Must Be Bisectable:** The largest addition says that every commit in a series must build and pass tests. Review fixes should therefore be folded into the commits where they belong instead of being added as follow-up commits at the end of a series.
* **Contributor Guidance Will Be Linked for Agents:** Stefano suggested referencing `CONTRIBUTING.md` from `AGENTS.md` so coding agents also follow the project's commit expectations. Jörg agreed to add that reference to the PR.

### Per-Commit CI Checks

* **Per-Commit Formatting and Clippy Checks Proposed:** Nicolai asked whether CI could run formatting and Clippy checks on every commit to enforce bisectability.
* **CI Runtime Impact Is Uncertain:** Carlos noted that the checks could further increase CI times, while Stefano suggested incremental builds might allow later commits to reuse much of the work from the first check.
* **Formatting Check Should Be Tried First:** The group leaned toward starting with per-commit `cargo fmt` checks, which should be relatively fast, and then measuring the additional cost of Clippy.
* **Commit-Size Trade-Off Noted:** Jörg cautioned that expensive checks on every commit could encourage contributors to create fewer, larger commits.
* **Tracking Issue Assigned:** Nicolai agreed to open an issue for the proposed per-commit CI checks.

### Follow-Up Work

* **OpenSSL Work Can Resume:** Oliver said he plans to resume his OpenSSL integration work. He already has a local version working but needs to clean it up and make it general enough to merge and test in SVSM.
