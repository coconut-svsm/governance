# Meeting Minutes: SVSM Development Call (November 27th, 2024)

## Attendees:

Adam Dunlap, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Tyler Fanelli, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Linux & QEMU Patches:

* IGVM patches reviewed and ready to merge.
* Stefano offered to help with the merge.
* Upstream plan for KVM/QEMU VMPL support changes discussed at KVM Forum.
* VTPM driver upstreaming in progress with Oliver and Claudio working on it.
* Joerg suggested adding Oliver's work to SVSM EDK2.

### Unsafe Block Documentation:

* Stefano documenting unsafe blocks with small PRs.
* Joerg offered to help review.
* Stefano opened a PR with a CI job to prevent new unsafe blocks.

### SVSM Status at FOSDEM:

* Stefano suggested an SVSM status update talk.
* James confirmed attendance at FOSDEM.
* Joerg encouraged Stefano to submit a talk proposal (deadline Sunday).

### Attestation Driver and Proxy:

* Tyler presented his PR for an attestation driver and proxy.
* Decision to keep the proxy in the SVSM repository for now, using tests to enforce protocol stability.
* Concerns about ABI and proxy's current host-side execution were discussed.
* RSA Key Generation Time:
  * Tyler noted slow RSA key creation.
  * James suggested potential issues with the Rust RSA crate and recommended OpenSSL.
  * Tyler will switch to using an elliptic curve instead.

### User Space Support:

* Clarification that TPM is loaded before guest start.
* No dedicated measurements for user-mode tasks.
* Plan for a reproducible build process with predictable launch measurement.
* Discussion on measured boot manifest.
* User Space Support Progress:
  * Vijay's pending PR should build on Joerg's user mode build PR.

### VirtIO-Blk and Attestation:

* Oliver continued working on the Virtio-Blk PR.
* Global Mapping API for MMIO:
  * Oliver reported successful testing.
* Possibility of storing disk encryption key in KBS.
* Attestation work needs to be finished first.
