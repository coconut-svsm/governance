# Meeting Minutes: SVSM Development Call (November 26th, 2025)

## Topics:

### TSC Update

* **Meeting Schedule:** There are only two TSC meetings remaining for the rest of the year. In December, the TSC will conduct a reflection on the project's progress.
* **PR Comment Resolution:**
    * Pull requests (PRs) can only be merged if all comments are resolved due to branch protection settings.
    * Only PR owners or those with write access can resolve comments.
    * PR authors are encouraged to resolve comments themselves if they believe an update addresses the issue.
    * Maintainers can override and resolve comments provided they supply a justification if the underlying issue is not addressed.
* **Ongoing Work:** The team discussed refactoring Stage 2 and C component building.
* **New Process Label:** A "TSC review pending" label was introduced.
* **Upcoming Release:**
    * A development release is scheduled for the last week of November.
    * Items marked with "release feature" are prioritized but are not strict blockers; if they are not merged by the cutoff, they will wait for the next release.
    * Jörg Rödel will begin creating the release PR tomorrow morning (European time).

### Technical Discussions

* **Scheduler Bug:**
    * Jon Lange identified a race condition in the scheduler using the `set_affinity` test.
    * **The Issue:** If the scheduler selects the idle task, it returns with interrupts enabled and then halts. An interrupt can trigger a new task readiness in the window between enabling interrupts and executing the halt, causing the system to halt incorrectly.
    * **The Fix:** The idle loop will be integrated into the scheduler.
    * **Timeline:** Jon plans to implement this fix within the next week, so it will not be included in the current release.

### PR Specific Updates

* **PR 855:** Jon Lange and Huibo Wang agreed this PR can be closed.
* **PR 881:** Jon Lange reviewed this PR and noted the fix needs adjustment.
* **Release Feature PRs:** Jon Lange identified Peter Fang as the blocker for two release feature PRs.
