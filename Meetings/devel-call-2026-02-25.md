# Meeting Minutes: SVSM Development Call (February 25th, 2026)

## Topics:

### **Testing and Rust Updates**

* Oliver Steffen proposed extending testing by utilizing the standard library for tests only, potentially enabled via a specific feature flag.
* The project has bumped the Rust version to 1.88, which Nicolai Stange noted introduces beneficial "syntax sugar".
* Oliver is currently working through the codebase file-by-file to apply Clippy recommendations and formatting updates.

### **Storage and TPM Persistence**

* There is an ongoing effort to progress on the persistence topic for the SVSM.
* The team discussed porting a proof-of-concept storage solution to wire up the TPM to storage.
* The reference TPM implementation reportedly writes a single 16KB file in full rather than supporting incremental writes, which may simplify the initial implementation.
* A goal was set to create a proof-of-concept to demonstrate disk encryption unlocking using these storage methods.
* There is interest in adding OpenSSL support for COCOON-FS storage, as the API has evolved since the BoringSSL fork.

### **Technical Steering Committee (TSC) Updates & Release Planning**

* Jörg Rödel summarized the TSC meeting regarding the upcoming release.
* Recent release testing identified a bug where SVSM dies at AP bring-up when compiled with release tag on QEMU with native platform.
* The team is reviewing PRs [#967](https://github.com/coconut-svsm/svsm/pull/967) and [#970](https://github.com/coconut-svsm/svsm/pull/970), but not target them for the next release.

### **Google Summer of Code (GSoC)**

* The COCONUT-SVSM Project has been accepted into GSoC under the QEMU project umbrella.
* Mentors will identify and mark "good first issues" in the SVSM codebase to help onboarding students.

### **Fuzzing and Issue Management**

* The team discussed [Issue #34](https://github.com/coconut-svsm/svsm/issues/34) regarding fuzzing.
* They plan to close [Issue #34](https://github.com/coconut-svsm/svsm/issues/34) and potentially create new sub-issues for specific interfaces, such as the guest-facing interfaces or versatile drivers.

### **Cross-Compilation and Linker Scripts**

* A significant discussion focused on cross-compiling x86 SVSM on ARM (e.g., MacBooks).
* Gerd Hoffmann noted that while C code cross-compiles easily, the Rust linker faces issues with current SVSM linker scripts, particularly regarding size calculations.
* Carlos López suggested the issue might be related to the "kernel" code model not being set for bare-metal targets.
* Jörg Rödel expressed openness to switching to the Rust linker as a separate PR to facilitate cross-compilation.
