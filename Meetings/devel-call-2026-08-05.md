# Meeting Minutes: SVSM Development Call (August 5th, 2026)

## Topics:

### TSC Meeting Update

* **PCID Management PR Discussed Again:** Jörg said the TSC revisited the PCID management PR 1157. After Jon clarified some details, Jörg said the PR looked fine.
* **PCID Bitmap Work Can Continue:** The TSC discussed bitmap infrastructure and noted that a larger bitmap rework is expected later, including support for atomic updates and atomic allocation of bit ranges. Until that work is ready, Tanish can continue adding a bitmap sized for PCID management.
* **Page-Table Crate Proposal Rejected for Now:** The TSC discussed the page-table crate proposal again and concluded that it is not a good idea to continue in the current direction.
* **Upcoming Page-Table Changes Conflict With the Split:** Jörg said the planned page-table changes will bind page-table code more closely to SVSM memory-management code, which conflicts with the goal of creating a cleaner standalone abstraction.
* **Observability Protocol Needs Spec Acceptance:** The TSC discussed the observability protocol PRs. Jörg said the protocol specification needs to be accepted before the related PRs can be merged, and he will take care of that.
* **MMIO Abstraction Direction Discussed:** The TSC discussed MMIO infrastructure and agreed that future MMIO work should move toward a better abstraction rather than only adding narrow fixes.
* **MMIO Mapping Ownership Needed:** Jörg said the desired abstraction should own the memory mappings used for MMIO and provide read and write methods, giving the code better ownership and lifetime tracking.
* **Different Platform Backends Expected:** The MMIO abstraction should allow different backends for different platforms. Jörg noted that TDX and SNP do not necessarily need actual page-table MMIO mappings because MMIO can be performed through GHCI or GHCB calls using GPAs.
* **No MMIO Owner Assigned Yet:** No one volunteered to work on the MMIO abstraction during the TSC meeting, so the direction is agreed but not actively assigned.
* **Contributor Commit History Discussed:** The TSC discussed recent PRs where contributors added separate follow-up commits for each review comment instead of folding fixes into the relevant original commits.
* **Clean History Expectations Should Be Documented:** The TSC wants to educate contributors, especially new contributors, to squash review fixes into the commits where they belong so that PRs maintain a clean history.
* **Contribution Documentation Needs Updating:** Jörg said `CONTRIBUTING.md` and related documentation are out of date and do not clearly describe the project's expectations for commit history.
* **Jörg Will Update Documentation:** Jörg took the task of updating the contribution documentation and expects to send a PR, possibly the following week.

### CocoonFS Status

* **CocoonFS PR Nearing Merge:** Jörg thanked everyone involved in the CocoonFS PR review and said the review is finished and the PR appears ready to merge soon.
* **Final Testing Planned:** Jörg said he will do some testing himself before the CocoonFS PR goes in.
* **Reviewers Thanked:** Jörg thanked Nicolai, Stefano, Luigi, Oliver, and others who worked on, reviewed, and tested the CocoonFS work.
* **SVSM Mode Feature Completeness Near:** Jörg said SVSM appears close to being feature complete for SVSM mode once this work lands.
