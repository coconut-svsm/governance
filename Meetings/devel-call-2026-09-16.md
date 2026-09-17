# Meeting Minutes: SVSM Development Call (September 16th, 2026)

## Topics:

### PCID Testing and Launch CPU Model

* **Launch CPU Model Needs an Update:** Luigi reported that the EPYC-v4 model used by the launch script does not expose the PCID and INVPCID feature bits. As a result, Tanish's PCID work cannot be exercised with the current launch configuration. Luigi suggested updating the model or exposed features.
* **Feature Detection Is Working:** Jörg noted that the behavior shows the PCID code checks the CPU feature bits before using the feature. The group did not settle whether the missing bits are a defect in the CPU model.

### TSC Meeting Update

* **SecureTSC Must Remain Optional:** The TSC discussed enabling SecureTSC through an IGVM builder parameter and using it only when the relevant SEV feature bit is present at boot. Keeping it optional leaves room to resolve possible incompatibilities with other architectural features. The group also noted that TDX has its own secure TSC mechanism.
* **Virtual-Memory Region Design Is Open:** Jörg's PR 1215 introduces a second VMR type with different semantics. The TSC discussed whether the types should be unified and how this fits the longer-term kernel memory-management design; no decision was reached.
* **Kernel Address Allocation Needs a Direction:** The current mix of static assignments and range-based allocation was compared with a more memory-efficient bitmap approach. The group will weigh the trade-offs before choosing how to proceed. Some static assignments are expected to remain.
* **Code Will Continue to Drive Design Review:** The TSC discussed when architectural questions should be raised. Contributors will continue to bring code for review and use design documents where helpful.
* **Per-CPU Rework Is Under Review:** Jörg's pending PR uses GS-based access and lets the linker gather per-CPU variables declared near their consumers. This could also remove variables for features excluded from a build.
* **GS Use Needs Further Planning:** The approach may affect entry code once user mode also uses GS for thread-local storage. This is not an immediate conflict, but the TSC will examine it during review and plan for future user-mode support.

### Shared Crypto Backend for Cocoon TPM and CocoonFS

* **Single Crypto Library Build Is Taking Shape:** Oliver's work now aims to link one instance of OpenSSL, or another selected crypto library, across the consumers discussed last week. The backend will be selectable on the Cocoon TPM side.
* **`libcrt` Moved to a Shared Crate:** Oliver moved the minimal C runtime out of the TPM crate into a top-level workspace crate so OpenSSL and the TPM code can use the same runtime library. It may be extended for other SVSM consumers.
* **Other TPM Crypto Backends Need Investigation:** James clarified that the Microsoft TPM implementation supports multiple crypto libraries, but building another one in SVSM's limited C runtime environment still needs work. Related UEFI work may offer reusable code, though its suitability has not been checked.
* **vTPM Will Select OpenSSL for Now:** Oliver plans for enabling vTPM to enable the OpenSSL backend automatically in his PR. Support for other backends can be added later.

### Linux and QEMU Host Branch Transition

* **Default Branch Switch Is Imminent:** Jörg plans to make the rebased downstream Linux and QEMU branches the defaults within two days. The branches are already available for testing; he described them as based on Linux 7.2 and QEMU 11.1.
* **Prepare for a Breaking SVSM Change:** Contributors were asked to update to the new host branches within the next week. Jörg expects to merge the SVSM-side breaking change, PR 1209, toward the end of that week. The delay gives users time to move off the older QEMU branch, which assumes a fixed VMSA guest-physical address.
* **Launch Measurements Will Temporarily Mismatch:** With the new host branches and the current SVSM, launch-measurement checks will fail until the corresponding SVSM change is merged. This affects configurations and tests that check launch measurements, including persistence tests.
* **IGVM Measurement Check Needs a Fix:** Stefano's testing found that an `igvmmeasure` check still expects the old VMSA address. Jörg said he would update his PR to fix the check. Stefano reported that the rest of his testing worked.
* **Report Further Regressions:** Jörg asked testers to email him about any other problems with the new branches.
