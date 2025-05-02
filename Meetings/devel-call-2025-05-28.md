# Meeting Minutes: SVSM Development Call (May 28th, 2025)

## Topics:

### TPM Driver Update

* The SVSM vTPM driver has been merged upstream into the Linux tree.

### Discussion on vTPM Protocol

* Dionna Glaze wants to discuss the progress on expanding the vTPM protocol to include the endorsement key template.
* James suggested inviting Tom Lendacky to the discussion.
* Stefano Garzarella will add the vTPM protocol discussion to the top of the agenda for the next meeting and Cc Tom.

### Nicolai Stange's Crypto Work and Attestation

* Stefano Garzarella inquired about the progress of Nicolai Stange's work on attestation and rebasing his work on crypto.
* Nicolai Stange plans to publish the crates on Crates.io and move the repository to the Coconut SVSM organization, pending Joerg's return from vacation.
* Nicolai Stange's next steps involve enabling the BoringSSL backend for the SVSM environment.
* Stefano Garzarella asked if OpenSSL will also be supported, as the TCG TPM implementation currently uses OpenSSL.
* Nicolai Stange stated that his current work only supports BoringSSL but he would implement an OpenSSL backend if there is demand.
* Dionna Glaze mentioned that the TPM reference implementation is rewriting its crypto interfaces.
* James emphasized the importance of reusing a single OpenSSL for both SVSM and TCG to avoid FIPS problems.
* Nicolai Stange noted that the difference between BoringSSL and OpenSSL for his purposes is how reference counts to objects are handled.
* For BoringSSL integration into the SVSM environment, per-CPU or per-thread storage is needed for the random number generator state.
* Nicolai Stange started with BoringSSL because Dionna Glaze mentioned it.
* Nicolai Stange hasn't tried OpenSSL recently but a year ago it seemed difficult to provide the required C environment in SVSM.
* Stefano Garzarella offered to help with the goal of having a single OpenSSL shared between SVSM and TCG, while also being open to supporting BoringSSL.

