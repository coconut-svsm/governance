# Meeting Minutes: SVSM Development Call (October 8th, 2025)

## Topics:

### SVSM Reboot Protocol and TPM

* Reboot Protocol Progress (Specification): Discussion centered on defining the reboot protocol and whether it should be published with or without the TPM reset component.
* TPM Reset Requirement: A core debate on whether the vTPM should be reset when the guest (VMPL2) initiates a reboot via the SVSM (Secure Virtual Machine Service Module).
* Security Implications of TPM Reset/Non-Reset:
  * Debate on whether resetting the TPM breaks the promise of an unreputable log for measurements, potentially broadening the attack surface through replaying SVSM measurements.
  * Architectural Constraints (RTMRs): Consideration of hardware differences, specifically Intel's RTMRs (Run Time Measurement Registers), which are tied to the lifetime of the virtual machine and cannot be reset without restarting the entire VM, making a full TPM reset unworkable for those architectures.
  * Pro-Reset Argument: Resetting the TPM is necessary to properly emulate a cold hardware reboot as expected by the guest operating system (VMPL2). This behavior is considered critical for mega data centers needing this feature now.
  * Con-Reset Argument: The TPM should not be reset because the full virtual machine context (including SVSM and devices outside the VMPL2 guest) is not being torn down. Resetting the TPM mid-VM lifetime breaks its promise as a repository for an unreputable log, especially in architectures like Intel's with RTMRs which cannot be reset.
* Specifying Reboot Behavior: Proposal for the reboot command to offer two modes: one that performs a TPM reset, and one that does nothing to the TPM.
* Conclusion on Path Forward:
  * The group acknowledged that determining the correct security properties of the TPM's initial state is a "long and complex discussion".
  * To make immediate progress on the reboot protocol, the suggestion was to proceed with the implementation that does not reset the TPM (the "don't touch the TPM" option), and continue the complex debate on TPM reset separately.
