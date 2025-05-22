# Meeting Minutes: SVSM Development Call (May 21st, 2025)

## Topics:

### OpenSSL 3.5 Integration:

* Oliver Steffen reported that his PR for OpenSSL 3.4.1 integration has been merged.
* His next goal is to integrate OpenSSL 3.5, but this requires fixes in OpenSSL for firmware environments (which are already merged but not yet released)
* A new release of the TPM library due to enforced version numbers is also needed.
* Jon Lange asked about potential issues with not yet running on 3.5, to which Oliver replied he wasn't aware of any.
* OpenSSL Performance Concerns: James Bottomley brought up recent reports about OpenSSL 3.5 performance problems.

### EDK2 OpenSSL Configuration:

* Oliver asked if the OpenSSL sys uaf configuration used by EDK2 could be leveraged for SVSM, as the environments are similar.
* James explained that enabling this would bring in EDK2 compatibility issues that SVSM doesn't have, especially with libc compatibility, requiring a lot more "shimming".
* He clarified that the printing routines in SVSM were taken from LibMusl, not EDK2.
* Oliver acknowledged there might be more work for shimming but noted that many things are disabled with the UEFI system in 3.5, which might make it worthwhile.

### LibMusl Version for Stripped-down C Library:

* Oliver inquired about the specific LibMusl version used for the stripped-down C library in SVSM, as he had to do additional work on it and couldn't find the exact origin in the commits.
* James stated that the code was "stolen" and significantly modified for the SVSM's debug port printing, and that Claudio would know the exact version.

### PR 702 (Rust Version Bump Fix):

* Stefano Garzarella mentioned PR 702, which addresses a CI failure when trying to bump the Rust version.
* The issue is with the unsafe block check pipeline, where tools for the older toolchain (1.84) are not being reinstalled when checking out the base branch.
* He noted that this PR should unlock other PRs. Jon Lange confirmed this was likely related to the issue he saw with PR 691.
* Jon will look at PR 702 for approval and merge today. After merging, PR 691 would need to be rebased and rerun.

### PR 655 (Read-Only IDT and GDT):

* Peter Fang brought up PR 655, which he has started reviewing.
* Oliver Steffen reported that it is not booting on SNP, and Peter cannot test on SMP.
* Jon Lange offered to do initial debugging, but noted his own previous tests showed it running, suggesting the issue might be specific to KVM and SNP.
* Oliver said he could assist but wasn't sure what to try.
* The debug output shows the system stopping after starting all 4 CPUs, with no panic.
* Jon suggested adding more logging and rebasing the PR on the latest changes. Peter confirmed he had already merged with main, and it still booted for him.
* Oliver will rebase and add debug output.
* Jon noted that the author of PR 655, Thomas Leroy, doesn't have SNP access, suggesting a need to find someone with an SNP system and knowledge of memory protection changes to take over.

### VMPL2 Guest Rebooting on SVSM:

* Richard Relph introduced himself and his work with AMD to get VMPL2 guests rebooting on top of SVSM.
* He has managed to get into OVMF after a reboot from Linux, but it fails quickly thereafter.
* Jon clarified that Richard's scenario involves making it look like a reset from VMPL2's perspective while VMPL0 stays up.
* vTPM and Attestation Concerns:
  * James immediately raised concerns about the TPM not resetting, leading to incorrect measurements and attestation issues.
  * Jon Lange echoed these concerns, emphasizing that vTPM guarantees its measurement state can't be reset without a full system reset, making a primitive in SVSM to reset measurements difficult to prove as secure.
  * James noted that a reset primitive exists in OVMF's SMI code, but it's not allowed in SVSM's vTPM scenario. If a reset mechanism is provably safe and causes OVMF to re-initialize, it could work.
* VMPL2 Disappearance on Reset:
  * James stressed that if there's no way to reset the vTPM without VMPL2 disappearing, it's fine.
  * Jon agreed, suggesting adding logic to SVSM to enforce a full reset.
  * James also asked how attestation would work, as there's no way to tell from the launch measurement that resets occurred.
  * Richard stated that attestation is a future aspect he hasn't reached yet but acknowledges it needs to work.
* OVMF in SVSM:
  * Jon explained that to ensure integrity, a private copy of OVMF needs to be stored in the SVSM address space during initial boot.
  * Upon reset, this pristine copy would be put back into the address space to make it appear as a fresh boot to VMPL2.
  * Richard confirmed that OVMF code pages can be modified during guest execution.
  * Jon added that memory occupied by OVMF can be reused by the kernel, further necessitating a private copy in SVSM.
* IGVM File and SVSM Filesystem:
  * Richard asked how much of the IGVM file (containing SVSM and OVMF) is loaded by QEMU versus SVSM.
  * Jon confirmed all of it is loaded by QEMU.
  * He clarified that SVSM can embed its own filesystem constructed at build time, which is inside the IGVM.
  * Jon suggested an idea where OVMF content is included in the IGVM file as unmeasured data.
  * The SVSM would then copy and hash this data during boot, with the hash embedded in SVSM's private memory for validation during resets.
  * James noted that the attestation of this hash would need to be handled.
