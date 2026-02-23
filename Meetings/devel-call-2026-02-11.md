# Meeting Minutes: SVSM Development Call (February 11th, 2026)

## Topics:

### **TSC Meeting Recap**

Stefano and Jon summarized the previous day's Technical Steering Committee (TSC) meeting:

* **LiteBox Project Introduction:**
  * Jon introduced "LiteBox," a new Microsoft Research open-source library OS that implements the Linux syscall ABI.
  * The goal is to target Litebox on top of COCONUT to provide a robust, confidential-first user-mode application model without needing a custom toolchain.
* **Security & Dependencies:**
  * The team discussed handling a security report from Dependabot regarding a broken dependency.
  * For indirect dependencies, they are currently updating `cargo.lock` and will begin running `cargo audit` during releases.
* **CI & Testing:**
  * Stefano proposed using `cargo hack` to stress-test feature combinations.
  * It was decided this will be run locally or before releases rather than in the standard CI to save time.
* **Formal Verification:**
  * A new CI label will be added to trigger formal verification manually.
  * Only users with at least a "triage" role can apply this label.
* **Feature Flag Review:**
  * Jon suggested reviewing existing feature flags (e.g., TPM protocol, VSOCK, VirtIO) to remove those that are no longer useful and reduce codebase complexity.
* **Stage 2 Removal:**
  * Jon is working on completely removing "Stage 2" code. Consequently, reviews for current Stage 2 changes will be less strict since the code is temporary.

### **Community & New Contributors**

* **GSOC Interest:**
  * Tanya Agarwal expressed interest in two Google Summer of Code (GSOC) projects: Process Context Identifier (PCID) and Linux-SVSM communication.
  * **GSOC Status:** The project is currently waiting for Google to announce accepted organizations; Coconut SVSM plans to run under the QEMU umbrella.
* **Getting Started:** Stefano recommended that new contributors without AMD SEV-SNP hardware use the native platform on QEMU to explore the codebase.
* **Hardware Access:** For projects requiring guest Linux booting (like observability), the team will look into providing interns with remote access to necessary hardware.

### **Technical Updates**

* **TPM Licensing:**
  * Stefano reported that the TCG merged a PR to fix a TPM license text issue.
  * It is now expected to be BSD-2-Clause compatible, and a corresponding PR has been opened for COCONUT-SVSM.
