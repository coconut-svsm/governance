# Meeting Minutes: SVSM Development Call (September 23rd, 2026)

## Topics:

### TSC Meeting Update

* **Stefano Chaired the Call:** Stefano hosted the development call because Jörg was ill and had also missed the previous day's TSC meeting.
* **PR Reviews Were the Main Focus:** The TSC reviewed current PRs and spent time on Carlos's page-table work. No further details or decisions were reported on the call.
* **QEMU TDX PR Needs Follow-Up:** The TSC discussed Peter's open TDX-support PR in the QEMU fork. Peter and Luigi will coordinate to decide whether to close or rebase it.

### Shared OpenSSL Implementation

* **Oliver's PR Appears Ready for Review:** Stefano reported that Oliver's PR appears to provide a single shared OpenSSL instance and is ready for review.
* **Additional Reviewers Are Welcome:** Stefano hopes to review the PR the following week and invited others to take a look as well.

### Conference Discussion

* **Several Contributors Expect to Attend KVM Forum:** The TSC discussed Linux Plumbers Conference and KVM Forum. Stefano expects several SVSM contributors to attend KVM Forum, and James confirmed that he will also be there.
* **An SVSM Gathering Remains Possible:** Stefano suggested organizing an SVSM-related gathering at KVM Forum. James noted that planes and VSM will be discussed there and that there should be time for related SVSM discussion. No concrete arrangement was made.

### Linux and QEMU Host Branch Transition

* **Breaking Changes Are Expected on Friday:** Stefano recalled Jörg's mailing-list announcement about the new Linux and QEMU branches and the accompanying SVSM PR. He expects the transition on Friday, September 25th, and reminded users that it introduces breaking changes.
* **Test the New Branches Before the Transition:** Contributors were encouraged to test the changes described in Jörg's email before Friday and report any issues by replying to that email.
