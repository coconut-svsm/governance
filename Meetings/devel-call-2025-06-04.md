# Meeting Minutes: SVSM Development Call (June 4th, 2025)

## Topics:

### Continued Discussion on Attestation Workflow and TPM Protocol Integration

* Key Points of Debate:
  * How TPM handles key creation and attestation (especially using volatile handles and deterministic primary keys).
  * Risks around resource management and limitations of volatile key slots in TPM.
  * Options to extend the vTPM protocol for a single, atomic “create-and-attest” operation.
* Consensus:
  * If operations remain internal to SVSM (as one atomic action), system behavior remains consistent.
  * A single SVSM command combining create and attest is acceptable if externally it behaves like an atomic call.
* Dionna Glaze’s Input:
  * Advocated for standardizing the command with TCG for broader compatibility.
  * Raised concerns about deviating from standard TPM user-space interfaces.
  * Proposed adding new protocol fields and manifest selectors for attestation.
* Implementation Details
  * Use Dionna's suggested approach where the manifest selector defines the attestation template.
  * Plan to implement this with new attributes in configfs.
  * Discussion of implementation strategy in SVSM, including use of volatile handles and caching logic.

### Kernel Version Compatibility and Rebase Discussion

* Luigi Leonardi:
  * Highlighted build issues with Linux fork on GCC 15.
  * Asked whether to rebase to 6.12 or the newly released 6.15.
* Jörg Rödel:
  * Suggests re-implementing based on Paolo’s KVM plane patches.
  * Goal: transition towards upstream-compatible infrastructure.
  * Warns of potential issues due to major changes between 6.11 and 6.16.
* James Bottomley:
  * Asked about rebasing on unmerged plane patches and risk of divergence.
  * Consensus: rebase and implement SEV-SNP support on top, even if upstream takes time.
* Interrupt Support and IRQ Handling in SVSM
  * One of the primary goals with VM plane support is to enable full interrupt handling:
  * Not only during boot, but also in the guest runtime.
  * Will reduce special cases and simplify the SVSM code base.

### QEMU and IGVM Support

* Discussion around integrating IGVM (used for guest memory management) in QEMU.
* Jörg Rödel:
  * Confirms that IGVM is QEMU-only and not a KVM change.
  * Notes progress stalled, calls for someone to pick up and rebase patches.
  * IGVM critical for making SVSM deployable in production.
