# Meeting Minutes: SVSM Development Call (July 29th, 2026)

## Topics:

### Release Update

* **New Release Announced:** Jörg said a new SVSM development release had been completed and announced on the mailing list.
* **Larger-Than-Usual Release:** The release included 122 commits, making it somewhat larger than usual.
* **Merging Can Resume:** Merging had been paused briefly for the release, but pending work can now continue.

### TSC Meeting Update

* **Release Discussed by TSC:** The TSC discussed the then-pending release, which has since been completed.
* **User-Space PRs Reviewed:** The TSC discussed user-space PRs 1165 and 1166. One had been merged, while the other was still waiting for Jörg's review and testing.
* **Page-Table Crate Split Deferred:** The TSC continued discussing whether to split paging code into a separate page-table crate. Jörg said the code is not ready for that split yet because substantial changes are still expected, and sharing it as a support crate would make those changes harder.
* **Future Page-Table Direction Still Open:** Whether the paging code should eventually become a separate crate remains subject to further discussion.
* **IGVM Image ID PR Looks Fine:** The TSC discussed PR 1175 for the IGVM image ID and generally agreed that the approach is fine.
* **IGVM Command-Line Support Discussed:** The TSC agreed that IGVM command-line support is useful, but discussed whether the command line should be measured.
* **Command Line Must Not Affect Security-Relevant Behavior:** Jörg noted that unlike the Linux command line, the IGVM command line will not be measured. It therefore must not be used for options that change security-relevant SVSM behavior.
* **Measured Boot Parameters Remain Available:** Security-relevant boot configuration can use the existing measured SVSM boot parameter block instead, while the IGVM command line is expected to be limited to debug-style options.
* **Observability Protocol Next Step:** The TSC discussed the observability protocol. Jörg will work with Tom on getting the protocol specification ready and into the official spec.
* **TOML Formatting CI Still Undecided:** The TSC again discussed whether TOML formatting should be enforced in CI. Some members preferred CI enforcement if formatting rules are adopted, while others were open to periodically running the formatter manually.
* **Formatter Tooling Has Practical Issues:** Building the TOML formatter in CI takes a long time, and dependencies need to be pinned by hash, which currently means building from a Git hash.
* **CI Alternatives Being Investigated:** The project is looking into alternatives, including an existing CI action, but no final decision was made.
* **TOML Cleanup PR Can Be Merged Separately:** Jörg said Oliver's TOML formatting cleanup PR is fine once rebased and limited to the TOML file updates. The `CONTRIBUTING.md` change should be kept for any later CI-enforcement work.
* **Other PRs Mentioned:** A fuzzer execution script and Stefano's release test plan update had both been merged. Other PRs were discussed briefly without major updates.

### KVM Forum Proposal

* **Project Overview Talk Proposed:** Oliver asked whether anyone planned to submit a COCONUT-SVSM topic for KVM Forum. If not, he planned to submit a last-minute abstract covering the project's progress over the past year and possible roadmap items.
* **Community Input Requested:** Oliver said he would collect topics from the community for the presentation.
* **No Competing Project Overview Submitted:** Jörg said he had not submitted a general project session and supported Oliver taking that on.
* **Jörg Can Provide Input:** Jörg said he had input for the proposed talk and encouraged Oliver to follow up with him.
