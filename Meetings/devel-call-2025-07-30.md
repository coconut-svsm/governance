# Meeting Minutes: SVSM Development Call (July 30th, 2025)

## Topics:

### Introduction of New PR Tags for Release Management

* Jörg Rödel introduced two new tags for Pull Requests (PRs) to facilitate the upcoming first development release, planned for next week (August).
* `Release-Blocker`:
  * PRs with this tag must be merged before a release can be made.
  * They typically fix important issues that need to be resolved.
* `Release-Feature`:
  * PRs with this tag are desired for inclusion in a release.
  * They will only be included if ready by the release date; otherwise, they will be omitted.
  * This tag serves as an indication for contributors to prioritize work on these PRs.
  * It's not a strict blocker, as development releases happen monthly, so delayed features can be included in subsequent releases.
* Discussion:
  * Stefano Garzarella suggested exploring GitHub milestones as an alternative to tags for release management, to avoid manually removing and adding tags for each release. He offered to investigate how milestones work in GitHub.
  * Jörg Rödel is open to better methods and appreciates the suggestion.

### KBS Attestation PR (#528) Merge

* Jörg Rödel announced that the KBS attestation PR (number 528) is ready for merge.
* Stefano Garzarella had previously approved it.
* Jörg Rödel conducted extensive testing, including the actual feature, and reviewed the code, finding everything satisfactory.
* He opened the floor for any last objections or comments from the community before merging this significant PR.
* No objections were raised.
* **Action**: The KBS attestation PR was merged during the meeting.
* **Acknowledgement**: Jörg Rödel thanked everyone for their continuous effort on this PR, acknowledging it was a long but worthwhile road and a significant collective effort. This PR will be part of the first development release next week.

### VSock Support in SVSM (RFC)

* Luigi Leonardi highlighted a new Request for Comments (RFC) he opened regarding introducing VSock support in SVSM.
* He has a proof of concept working, based on the recently merged attestation PR.
* The current implementation attempts to use VSock first if enabled, falling back to the serial port if issues arise. The behavior can be adjusted.
* Luigi emphasized that the code is not yet perfect and is open to suggestions and feedback. Some parts still require refactoring.
* Jörg Rödel confirmed his understanding that VSock is an alternative to the serial console for host communication and will review the PR, providing feedback.
* Stefano Garzarella also reviewed the PR and plans to provide more detailed feedback.

### Verification Efforts Prioritization

* Ziqiao Zhou thanked Stefano Garzarella for his useful feedback on the verification PRs, noting that the PR looks much better now with only minor changes remaining.
* Query from Ziqiao Zhou: She inquired if there are any modules or components that the SVSM team would prioritize for verification, or if she should continue with her original plan:
  * Allocator part
  * Page table
  * Protocol
* Discussion & Guidance:
  * Stefano Garzarella found Ziqiao's original plan acceptable.
  * Jörg Rödel suggested prioritizing the protocol implementation over the page table implementation.
    * Reason: Upcoming changes to the page table implementation might make verification work harder or require updates after changes are made.
    * Prioritizing the protocol, which is more static currently, would avoid stepping on each other's toes.
    * Ziqiao Zhou acknowledged this and will investigate the feasibility, noting that sometimes the protocol part might depend on the page table, requiring some page table specification.
  * Jörg Rödel mentioned that the allocation verification PR is marked as a "`Release-Feature`," indicating a good chance of inclusion in next week's release if ready by the end of the week.
   * Ziqiao Zhou expects to fix all current comments today.
   * Jörg Rödel clarified that fixes found by verification that require changes to the actual code are expected and fine.
   * Future Recommendation: For future verification efforts, Jörg Rödel suggested separating fixes into distinct PRs from the verification additions to simplify the review process.
