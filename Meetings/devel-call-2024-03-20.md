# Meeting Minutes: SVSM Development Call (March 20, 2024)

## Attendees:

Adam Dunlap, Carlos López, Cláudio Carvalho, Elena Reshetova, Huibo Wang, James Bottomley, Joerg Roedel, Nicolai Stange, Oliver Steffen, Roy Hopkins, Stefano Garzarella, Vasant Karasulli

## Topics:

### vTPM Merge

* Joerg Roedel plans to merge the vTPM code into the kernel.
* Cláudio Carvalho will address minor code review comments and test the updated TPM driver.
* Discussion about whether to compile vTPM code into the kernel or have a separate binary with configuration options.
* Consensus is to for now have different IGVM files for different configurations and potentially separate binaries depending on Cloud Service Provider (CSP) needs.

### Early Attestation and Measurement Architecture

* Joerg Roedel proposes creating a document to define a secure measurement architecture for early attestation in the SVSM.
* Volunteers include Stefano Garzarella, Roy Hopkins, Cláudio Carvalho, Elena Reshetova and potentially others.
* The document will focus on:
  * Threat model and what needs protection
  * Early key injection into the SVSM from an external, trusted source
  * Communication between guest VMs and the KBS (Key Broker Service) or attestation service
  * Discussion about using a generic interface for the guest VM to communicate with the hypervisor and whether the SVSM needs to be involved.
  * Need to consider different attestation service options.
* There are open questions about how to securely provision identities and secrets in VMs.

### Joining Confidential Computing Consortium

* Joerg Roedel received approval from SUSE to move forward.
* Some open questions need to be resolved, but onboard can probably be completed in the next weeks.
