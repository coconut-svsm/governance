# Meeting Minutes: SVSM Development Call (July 22nd, 2026)

## Topics:

### CocoonFS Review

* **CocoonFS PR Review Started:** Luigi said he had started reviewing Nicolai's CocoonFS PR shortly before the meeting.
* **Commit Title Style Needs Checking:** Luigi noted that some commits may not follow the project's usual `subsystem: summary` title style. Nicolai said he would recheck them and could fix them during a rebase if needed.
* **Clippy Warning Discussed:** Luigi mentioned a Clippy issue around unused code in an early commit. Nicolai said the code is introduced for use by a later commit, but he would check whether an `allow` should be added and then removed in the follow-up commit.

### TSC Meeting Update

* **Open PRs Reviewed:** Stefano said the TSC mostly reviewed the current PR status and did not make major decisions.
* **User-Space PRs Still Waiting for Jörg:** The TSC would like to wait for Jörg's return before merging Nicola's user-space work.
* **IGVM Boot Parameters Still Waiting on Spec Work:** Jon updated the TSC on boot-parameter and IGVM work. The related PR remains a draft while the project waits for Chris Oo from Microsoft to improve the IGVM spec, including optional parameter support and related CoRIM support.
* **PCID PR Should Explain Draft Status:** Tanish said the PCID PR depends on another CPUID PR. Luigi had suggested keeping the PRs separate and rebasing whichever one remains after the first is merged. Stefano asked Tanish to document the dependency in the PR so reviewers understand why it is still a draft.
* **Observability Protocol Needs Documentation:** Stefano said Nicola's Observability Protocol work should include documentation of the observability objects exposed to the guest. This should make the interface easier for maintainers to review.
* **CPUID Review Planned:** Carlos and Peter are expected to review Tanish's CPUID work.
* **KBS and CocoonFS-Dependent Work Await Review:** Stefano said Arun's KBS support improvements still need review, and two other PRs appear to depend on the CocoonFS work.
* **Multiple Waiters Work Being Followed Up:** Jon is discussing the multiple-waiters-on-wait-queue work with the author.
* **Page-Table Discussion Continues:** The TSC discussed the page-table work at length but did not reach a decision. The topic is expected to continue the following week.
* **TOML Formatter CI Decision Deferred:** The TSC still wants TOML formatting covered by CI, but Jörg had raised concerns about binary downloads. The group will wait for Jörg's return before deciding how to proceed.
* **vTPM PR Is Stale:** Stefano noted that the vTPM PR has become stale.
* **Device-Tree Compatibility Being Checked:** Jon is checking whether the device-tree work functions correctly with Hyper-V.
* **Attestation PR Needs Testing and Review:** Stefano said he will look at the attestation PR, which came from an unfinished Google Summer of Code project.
* **CocoonFS Review Is a Priority:** Stefano said the CocoonFS PR will be reviewed as soon as possible.

### IGVM Device Tree and Vanadium

* **Vanadium Ignores Optional Unknown Directives:** Luigi asked how Vanadium handles IGVM directives it does not implement. Adam said Vanadium ignores unknown optional directives but fails to load if an unknown required directive is present.
* **Vanadium Does Not Currently Support Device Trees:** Adam said Vanadium does not currently support device trees. If the device-tree directive is marked mandatory, Vanadium would fail to load the image.
* **Optional Directive Support Is Needed in IGVM Builder:** Stefano said the IGVM Builder currently cannot mark a directive as optional, which is part of the work Chris Ho is expected to address.
* **Empty Device Tree May Be Sufficient:** Adam said full device-tree support in Vanadium would be difficult because Vanadium does not use device trees for other VMs, but passing an empty or very simple device tree should be easy to implement.
* **SVSM Can Tolerate a Malformed Device Tree:** Luigi said the current PR ignores malformed device trees, so an empty or minimal device tree from Vanadium would be acceptable.
* **Vanadium Will Add Minimal Support When Needed:** Adam said Vanadium can implement the required minimal support when it next merges with upstream.
