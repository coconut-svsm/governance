# Meeting Minutes: SVSM Development Call (March 12th, 2025)

## Attendees:

Adam Dunlap, Dionna Glaze, Geoffrey Ndu, Huibo Wang, James Bottomley, Joerg Roedel, Nicolai Stange, Peter Fang, Stefano Garzarella, Thomas Leroy, Tom Lendacky, Vasant Karasulli

## Topics:

### Shadow Stack PR Issues on KVM:

* Joerg Roedel reported that a shadow stack PR posted by John Lang caused boot failures on SVSM after trying to use shadow stacks on KVM due to KVM shadow stack emulation not being implemented.
* Enabling shadow stack emulation for KVM SEV-SNP guests was implemented by disabling the MSR intercepts.
* A merged PR in the Linux kernel repository addresses this issue. Users need to update their host Linux to run the latest SVSM on KVM.

### Firmware UKI Project and Boot Methods:

* A discussion arose about supporting only IGVM as a boot method for the COCONUT-SVSM project.
* The firmware UKI (F-UKI) project, by AWS and RedHat, proposes a firmware config interface for VM firmware updates, which appears limited compared to IGVM.
* Dionna Glaze noted that F-UKI might not cover all necessary cases, such as classifying the CPUID page for SEV-SNP.
* Concerns were raised about the lack of support for specifying a VMSA page and the guest memory layout in UKI.
* Paolo is reportedly working on changing KVM to reconstruct the SEV context on reset without VMM intervention, which could impact the firmware replacement protocol.
* Discussion covered the implications of an x86 default reset state VMSA and its potential impact.
* It was suggested to discuss these efforts in the CCC kernel SIG meeting or the platform meeting.

### VTPM Attestation and Protocol:

* Discussion on vTPM attestation, single service attestation updates, and the send command protocol with size information.
* Dionna Glaze is building a single service attestation implementation depending on TPM.RS.
* James Bottomley raised concerns about the dependency on TPM.RS due to its slow progress.
* Alternatives like Parallax libraries and Nikolai Stange's interface generator were discussed for marshalling/unmarshalling code.
* Tom Lendacky questioned the need for an additional attestation command and how to specify templates.
* Discussion about using an empty authorization for getting the public key out of the simulator.
* Stefano Garzarella asked about the current TPM driver and whether it's okay to always pass a page to cover the entire ether plus buffer.
* It was decided that the send command buffer should be restricted to a page.
* James Bottomley confirmed that the TPM has a maximum size of 3968 bytes, which is under a page.
* Tom Lendacky suggested a copy-to-user API to catch buffer size issues, but Stefano Garzarella pointed out that the buffer size can vary.
* Discussion about using guest physical addresses for the SVSM-TPM protocol.
* Tom Lendacky mentioned a mechanism to check the protocol version and suggested a new protocol for larger buffers if needed.
* Stefano Garzarella asked about the vTPM protocol versioning and how it's checked.
* It was decided to update the spec to state that a page should be used for the buffer.
