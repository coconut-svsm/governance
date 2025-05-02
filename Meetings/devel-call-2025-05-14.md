# Meeting Minutes: SVSM Development Call (May 14th, 2025)

## Topics:

###  Introduction of the Technical Steering Committee (TSC)

* Jörg Rödel announced the formation of the Technical Steering Committee (TSC) for the COCONUT-SVSM project.
* The purpose of the TSC is to:
  * Distribute project maintenance.
  * Increase the project's bus factor.
  * Help with PR reviews, testing, merging, and strategy issues.
  * Provide a venue for architectural discussions and decisions.
* TSC members include Jörg Rödel (chair), Peter Fangs, Stefano Garzarella, and John Lang.
* TSC members have write access to the COCONUT-SVSM repository, with a rule requiring one approval from a TSC member before merging any PR.
* The TSC plans to grow as the project matures.
* Decision-making in the TSC involves discussions and voting (yes, abstain, no), with no constituting a veto. The TSC chair can override a veto in exceptional circumstances.
* Meeting decisions will be documented and published in the Governance Repository.
* Jörg Rödel will be taking vacation for the next two weeks. Jon Lange will run next week's meeting, and Stefano Garzarella will run the meeting on May 28th.
* The TSC will discuss and decide on the code of conduct enforcement.

### VirtIO-Block Device Persistent Store Backing

* Dionna Glaze raised the issue of providing persistent store backing for the VirtIO block device, specifically regarding flushing behavior for UEFI variables and vTPM.
* Oliver Steffen acknowledged the need for further discussion on what needs to be flushed and when.
* Dionna Glaze suggested having separate block devices for UEFI variables and vTPM to manage network traffic.
* James Bottomley discussed the variability of data updates for UEFI variables and TPM, and the complexities of ensuring rollback safety for persistent storage.
* Dionna Glaze mentioned a proposal for a trusted source of time to address rollback issues, presented at the Virtual Platform Working Group at the TCG.
* The discussion touched on TPM revision updates and post-quantum cryptography considerations.

### Rust Version Update

* Jörg Rödel inquired about any objections to merging the PR to increase the rest version to 1.86.
* Dionna Glaze confirmed that rebuilding the toolchain container with 1.86 should be fine.
* The potential impact of Rust version updates on code verification was discussed, including the need to update tooling.
* Luigi Leonardi reported an incompatibility issue with Verus and the current rust version (1.84).

### Multi-Service Attestation and SVSM Protocol Discussion

* Dionna Glaze discussed a conversation with Tom about the single service extended protocol extension.
* Tom requested a simplification to avoid generating the key as part of attestation, suggesting instead to provide a handle to the key.
* Dionna Glaze proposed using the qualified name and reading the public key to ensure it's a primary key before providing the public key in the manifest.
* James Bottomley agreed that the qualified name is sufficient but noted the increased complexity of verifying it within the SVSM.
* Dionna Glaze also considered a slot-based configuration resource for enumerating multiple services, but James Bottomley expressed concern about added complexity and questioned the value.
* The discussion also covered the timeout issue related to key generation and potential preemption handling.
