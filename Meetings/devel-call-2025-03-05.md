# Meeting Minutes: SVSM Development Call (March 5th, 2025)

## Attendees:

Cláudio Carvalho, Dionna Glaze, Huibo Wang, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tom Lendacky, Vasant Karasulli

## Topics:

### US Time Zone Shift:

* Joerg Roedel informed the participants that the US would switch to summertime next weekend.
* SVSM Call is scheduled in CET timezone.
* There is a one-hour shift of meeting time for US participants in the next three weeks.

### COCONUT-SVSM Chat Room:

* The participants discussed the need for a chat room for the project.
* Options like Slack, Discord, and Matrix were considered.
* Joerg Roedel expressed a slight preference for Slack and offered to explore creating a channel within the Confidential Computing Consortium's Slack workspace.

### QEMU IGVM Updates:

* Stefano Garzarella reported an issue with the latest QEMU IGVM support during the initialization phase.
* He is working on a fix and will coordinate with Roy and Paulo to get it merged before the freeze on March 11th.

### VirtIO Block Effort:

* Oliver Steffen provided an update on the VirtIO block effort, mentioning a new PR with the VirtIO drivers crate included as a local subcrate.
* He also discussed using the hardware info file for MMIO address communication from QEMU.
* He is currently working on improving the tests for the block device.

### Attestation PR:

* Joerg Roedel acknowledged the pending attestation PR and noted that it, along with the VirtIO block PR, is a significant step towards achieving persistence.
* Stefano Garzarella suggested looking into Open VMM for existing tools related to file systems and TPM manufacturing.

### Native Platform Support:

* Joerg Roedel shared an update on the native platform support, stating that it is now working with a fix for an IPI issue.
* He believes this will make development easier and more accessible to contributors without special hardware.
* The participants also discussed the possibility of emulating VMPL in QEMU, which could be a potential project for Google Summer of Code.

### PR 584 and Safety Comments:

* Joerg Roedel announced that PR #584 (adding safety comments to kernel CPU) is ready to merge and may require adjustments to other pending PRs. 
* He requested that developers review and rebase their PRs as needed.

### TPM and VTPM Driver Discussions:

* Selector Semantics for Single Service Attestation:
  * Dionna Glaze shared their work on implementing selector semantics for single-service attestation.
  * They plan to collaborate with Stefano Garzarella for end-to-end testing.
  * They also mentioned the need to specify key templates at non-volatile indexes and to figure out how to easily embed and swap out binaries. 
  * A discussion followed on integrating with Geoffrey's work, the potential use of the TPM.RS project's libraries for marshalling and unmarshalling, and the need for the libraries to support `no_std`.
* Missing Length Argument and TPM Commands:
  * A discussion regarding the missing length argument for sending commands to the TPM ensued, involving Dionna Glaze, Stefano Garzarella, and Cláudio Carvalho.
  * They determined that the TPM command and response structures use type-length-value encoding, eliminating the need for a separate length argument.
  * However, they agreed the current system is limited to a single page, and future protocol extensions may be needed to handle larger buffers.
* SVSM Linux Driver State and EDK2 TPM Driver
  * Stefano Garzarella provided an update on the SVSM Linux driver, aiming for a V3 release that week.
  * Dionna Glaze indicated that they were comfortable merging the EDK2 TPM driver based on the agreement on the Linux side.
