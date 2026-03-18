# Meeting Minutes: SVSM Development Call (March 18th, 2026)

## Topics:

### **QEMU and Device Tree Support**

* Update on the progress of the Device Tree support pull request (PR) and its relationship to QEMU versions.
* The current work is based on a rebase by Oliver and incorporates useful changes in IGVM processing from upstream QEMU.
* The team decided to wait for the release of QEMU 11 (expected next month) before merging these updates, rather than taking an intermediate step with version 10.2.

### **GitHub Workflow PR Improvements (PR 1003)**

* Discussion regarding a PR intended to improve security and maintainability of GitHub workflows.
* The PR involves pinning dependencies by Git commits (GitHash) rather than tags to align with OpenSSF Scorecard recommendations.
* A concern was raised that Git commits are harder to manage manually for contributors.
* Jörg noted that an online tool exists to convert workflows to this format and will document this process in the PR to assist future contributors.
* Workflow permissions will also be reduced to the minimum required for each task.

### **PackIt as a Cargo Dependency vs. Git Submodule**

* A debate over whether to change PackIt from a Git submodule to a cargo dependency.
* **Developer Ergonomics:** Jon Lange argued that keeping it as a submodule is better for active development, as it allows simultaneous changes to both PackIt and SVSM without breaking local references or requiring temporary `Cargo.toml` edits that cannot be submitted.
* **Cargo Dependency Benefits:** Carlos López argued that using cargo commands to redirect to a local copy is straightforward and "cleaner" than managing submodules.
* **Future Development:** Jon Lange noted that PackIt is expected to undergo significant active development over the next year (e.g., user mode and file system support), making the submodule approach more practical for now.
* **Alternative:** The group briefly discussed moving PackIt entirely into the SVSM repository or keeping it as a submodule but referencing it as a library in the workspace.

### **IGVM Tools Separation**

* Briefly touched upon the potential for moving certain tools out of the main repository.
* While IGVM Measure could potentially be a separate tool, IGVM Builder is currently too tightly integrated with SVSM internals to be moved.
* In the long run, much of the functionality in IGVM Measure may move into the IGVM crate itself.
