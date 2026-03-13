# Meeting Minutes: SVSM Development Call (March 11th, 2026)

## Topics:

### **OpenSSF Scorecard Improvements**

Jörg Rödel provided an update on Issue 283 regarding the project's OpenSSF Scorecard shortcomings.

* **Permissions and Dependencies:** A recent [PR](https://github.com/coconut-svsm/svsm/pull/994) was initiated to fix workflow permissions and pin dependencies to specific commits rather than version tags.
* **Static Analysis:** CodeQL has been enabled for the SVSM repository. However, the initial CI check failed due to default build assumptions that do not apply to the project; further manual updates are required.
* **Release Signing:** Current releases are not signed. James Bottomley suggested using Sigstore for automated, transparent signatures within the CI workflow. Jörg noted that while release tags are already signed, the tool specifically flags the lack of signatures on generated tar and zip files.

### **Packaging and Distribution Workflow**

The team discussed the necessity of providing official tar files for downstream consumers.

* **Dependency Issues:** Standard GitHub-generated tar files are currently of limited value because they do not include submodules or vendored dependencies.
* **Downstream Impact:** Luigi Leonardi (Red Hat) noted that for Fedora, they generally do not use vendored dependencies and often apply downstream patches anyway.
* **Decision:** The team decided to leave the current process as is for now. They will consider either disabling the signed releases check or finding a way to prevent GitHub from automatically creating incomplete tar files until a more useful packaging pipeline is established.

### **IGVM Measure Tool**

The Technical Steering Committee (TSC) discussed proposal to move `igvm_measure` to its own standalone repository.

* **Use Case:** Oliver Steffen explained that the tool is currently the only generic way to calculate measurements for IGVM files, such as when wrapping OVMF for SEV-SNP launches.
* **Maintenance:** The TSC is in favor of the move, provided there are contributors willing to maintain it as a separate tool and library for broader use cases.

### **Technical Discussion: Rust Formatting and SPDX**

* **SPDX Checks:** Luigi Leonardi proposed adding an SPDX license header check to the CI. Nicolai Stange expressed interest in cherry-picking this for the Coconut TPM repository once merged.
* **Rust Formatting:** The SVSM repo currently runs `cargo fmt --check`. Nicolai plans to re-enable similar checks in the TPM repository.
