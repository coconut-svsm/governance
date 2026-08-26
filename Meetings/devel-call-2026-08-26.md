# Meeting Minutes: SVSM Development Call (August 26th, 2026)

## Topics:

### TSC Meeting Update

* **Security Fixes Merged for the August Release:** Fixes for two security advisories have been merged into the upstream branch in time for the upcoming release.
* **Advisories Will Follow the Release:** The fixes had remained under embargo while they were pending. The advisories themselves will be published once the release is available.
* **Page-Table Changes Discussed:** The TSC continued discussing the planned page-table rework and its trade-offs. More details are expected when Carlos posts the corresponding PR.
* **Portable Machine Image Format Raised:** The TSC was made aware of Portable Machine Image (PMI), a proposed alternative to IGVM. Jörg plans to study it further and speak with its proposer.
* **PR and Issue Reviews Are in Good Shape:** The remainder of the TSC meeting covered routine pull-request assignments and issue review, with no major blockers identified.

### August Release

* **Release PR Opened for Testing:** Jörg posted the August release PR shortly before the call and asked the community to test it and report anything unexpected.
* **Initial Testing Passed:** Jörg's own release testing, including the fuzzers, completed successfully.
* **Approval Requested:** The release PR still needs an approval before Jörg can merge it and publish the release. Carlos agreed to review and test it.

### Observability Protocol

* **Protocol Number Agreed:** Jörg met with the specification reviewers, and they settled on a protocol number.
* **No Major Specification Concerns Remain:** The reviewers had no major concerns with the protocol after the changes discussed during the latest mentoring call.
* **Protocol Number PR Can Merge After the Release:** Jörg plans to handle the merge once the August release is complete.
* **Official Specification Update Will Take Longer:** Incorporating the protocol into the official SVSM specification is expected to take another two or three weeks.
* **Nicola Will Receive the Current Draft:** Jörg will send Nicola his latest version of the specification so Nicola can align the implementation with the protocol changes in the meantime.

### SecureTSC Support

* **SecureTSC PR Submitted:** Jörg thanked Vasant for posting the SecureTSC PR.
* **Remaining CI Failures Appear Minor:** The PR still has CI failures, but Jörg expects the required fixes to be straightforward.
* **SecureTSC Must Be Optional:** Support needs to remain optional because CI also runs native configurations where SecureTSC is unavailable. Jörg noted that TDX likely requires similar handling.
