# Meeting Minutes: SVSM Development Call (October 1st, 2025)

## Topics:

### Update from the Technical Steering Committee (TSC) Meeting

* Planes Work Status:
  * The planned September release of planes patches did not happen because the code is not yet fully booting; it stops at a certain point.
  * Debugging is ongoing to determine why this is the case.
  * The work will be pushed out once it successfully boots.
* Pull Request (PR) Updates:
  * The [MMIO for native platform PR](https://github.com/coconut-svsm/svsm/pull/775) was found ready and has been merged.
  * [github/workflows: Enable test-in-svsm for NOCC #823](https://github.com/coconut-svsm/svsm/pull/823) was discussed.
    * It was confirmed that the PR does not significantly increase the total CI time because it removes a previous native boot test.
    * The Rust pipeline takes about 9 minutes, and the QEMU pipeline takes 2 minutes, running in parallel.
    * The PR still requires review.
* Dependabot Integration:
  * There was a proposal to use Dependabot, a GitHub tool that regularly checks dependencies for security vulnerabilities and updates them.
  * The team decided to perform some experiments first before fully enabling the tool, partly due to initial concerns about auto-committing capabilities.
* [EDK2 and IGVM](https://github.com/coconut-svsm/svsm/pull/824):
  * The EDK2 changes for IGVM need to consider parallel changes to EDK2 coming from Gerd.
* [SVSM Development Plan](https://coconut-svsm.github.io/svsm/developer/DEVELOPMENT-PLAN/):
  * The team started updating the existing development plan document.
  * The goal is to update it, remove completed items, and reorganize remaining items to bring it to the newest state.
  * The "observability" item will likely be promoted to a top-level category with sub-items.
  * The finalized plan will be moved to GitHub issues or projects for official tracking.
  * The updated plan will also serve as a source for a list of work items for potential new contributors (e.g., Google Summer of Code or CCC internship programs).

### Next Meeting Lead:

* Jörg Rödel announced he will be traveling and unable to run the meeting on October 8th.
* Stefano Garzarella volunteered to run the next meeting.

### SNP Machine for CI:

* There is no update yet on acquiring an SNP machine to run CI.
* Jörg is still waiting for internal feedback regarding a possible machine donation.

### [VSOCK PR](https://github.com/coconut-svsm/svsm/pull/766) and Device Tree:

* Luigi Leonardi's VSOCK PR is currently on hold because it is blocked on a device detection capability in SVSM.
* Device tree work is needed but has not been started yet.
* Jörg suggested Luigi could work on an SVSM-specific device tree by making changes to QEMU to create a device tree with SVSM-only devices for consumption by SVSM.
* Jörg expressed a reservation about merging more device tree changes without SVSM detection functionality.
* Stefano noted that this device tree work could also be reused for Virtio-Block and moving SVSM logging off the serial port.

### TPM Reset and [Guest Reboot](https://github.com/coconut-svsm/svsm/pull/808):

* Richard Relph raised an open question from a review about TPM reset during a guest reboot (related to the RLE bits PR).
* The security rationale of a TPM is that PCRs cannot be reset except under restricted state transitions; a warm restart (like Kexec) does not reinitialize the TPM, but a cold reset does.
* The issue is that the PR deals with restarting the VMPL2 firmware (a cold restart equivalent for the guest) without restarting the SVSM.
* The proposed solution is to wire the TPM `init` functionality to a cold reset of just VMPL2, which the SVSM could supervise, provided the SVSM does not measure into the Virtual TPM (VTPM).
* It was confirmed that while SVSM does not currently measure into the VTPM, OVMF's image does get measured by OVMF itself.
