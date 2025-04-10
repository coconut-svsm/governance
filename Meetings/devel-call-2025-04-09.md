# Meeting Minutes: SVSM Development Call (April 9th, 2025)

## Topics:

### SVSM Protocol Specification Update:

* Discussion on a proposed update for the single attestation extension.
* Concerns raised about the discriminator and the use of TPM templates.
* Tom Lendacky agreed to review and update the spec.
* James Bottomley suggested considering an open-source approach for the spec.

### SVSM Bus:

* Discussion on the SVSM protocol and communication mechanism, including the potential for sub-protocols and architecture-specific protocols.

### Trusted Execution Environment (TEE) API:

* Discussion about the [GlobalPlatform.org](https://globalplatform.org/specs-library/?filter-committee=tee) specification and its potential relevance to SVSM.

### Attestation PR ([Add support for SVSM attest protocol](https://github.com/coconut-svsm/svsm/pull/662)):

* Discussion on updating an attestation PR, including addressing memory safety and code review by Geoffrey Ndu.

### SEV-SNP Alternate Injection Support:

* Matthias Griebl inquired about the status of SEV-SNP alternate injection support.
* Tom Lendacky provided an update on the ongoing development and dependencies.

### SVSM Development Mailing List:

* Joerg Roedel announced plans to move the mailing list to lore.kernel.org for better archives and management.

### Random Number Generator and Stack Usage ([PR 528](https://github.com/coconut-svsm/svsm/pull/528)):

* Discussion on high stack usage in the attestation PR, particularly related to the random number generator.
* Nicolai Stange offered an alternative implementation.
* Potential solutions for high stack usage, including temporary stacks, were discussed.
* Discussion on moving services to user space to avoid stack usage issues.
