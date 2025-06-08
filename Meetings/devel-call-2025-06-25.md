# Meeting Minutes: SVSM Development Call (June 25th, 2025)

## Topics:

### Live Migration Discussion

* Stefano Garzarella (Red Hat) initiated a discussion on live migration, seeking to understand current status and potential areas for community help.
* Tom Lendacky (AMD) provided an update:
  * It's a complex ongoing effort requiring "plane support."
  * Involves tracking validated memory within the SVSM, packaging and sending data, and destination testing.
  * Currently focused on a functional proof of concept, not yet involving attestation.
  * Attestation for live migration is expected to be "very interesting" and potentially controversial, especially with different machine types and SVSM levels.
  * Noted that guest owners are typically not involved in live migration, but may need to be with SNP and attestation, which some cloud providers may dislike.
  * Will check with Pankaj (who is driving live migration) to identify specific areas where the community can assist and will try to get him on the next call for a more detailed overview.
* James suggested separating the migration engine from attestation to allow earlier release and testing of migration without being tied to specific attestation methods.
  * Proposed a three-stage difficulty: actual migration, guest policy for migration, and attestation.
  * Jakub Ruzicka mentioned he is writing his thesis on live migration, specifically on the validation of pages in the SVSM and transferring pages with keys between migration agents. He is not currently solving attestation issues.
  * Tom Lendacky clarified they are not planning on using migration agents.
  * Jakub expressed willingness to help and will post on the mailing list to coordinate efforts.

### Rebasing QEMU Branch

* Vaishali Thakkar asked about rebasing the QEMU branch (specifically QEMU 10) for her two security patches. She wanted to confirm she wouldn't be stepping on anyone's toes and if anyone else was working on it.
  * Jörg Rödel confirmed that rebasing is appreciated.
  * He attempted a rebase onto QEMU master to debug a Linux boot issue (hanging at some point), which he believes is not related to the IGVM patches but possibly to the 6.11 kernel and new QEMU.
  * Encountered issues with other patches on their current QEMU branch, as they rely on features from the 6.11 SVSM kernel that are not yet upstream (e.g., direct setting of the VMSA).
  * Encouraged Vaishali to proceed if she has time, and to report on her progress.
* Stefano Garzarella (Red Hat) asked if the upstream TPM driver (now in 6.16 kernel) should be backported to our 4 (their Linux branch).
  * Jörg Rödel suggested documenting that for guests, an upstream kernel should be used. He tests with an upstream kernel in his guest image, and when 6.16 hits rolling distros, people can use those images out of the box.

### Undocumented Unsafe Blocks

* Jörg Rödel raised the recurring topic of undocumented unsafe blocks, emphasizing the need to reduce their number.
* He will focus on the memory management part.
* Stefano Garzarella (Red Hat) stated he would post an issue with a report and open a PR with scripts to help.
* Currently, there are approximately 180 undocumented unsafe blocks:
  * ~146 under kernel/
  * ~62 in mem (memory management)
  * ~30 in cpu
  * Others in pods, virtio drivers.
* The goal is to reduce them to zero to enable permanent linting and simplify the CI process.
* Invited everyone to help and to coordinate by sending a short note to the mailing list to avoid duplicate work.

### Development Machines for Contributors

* Stefano Garzarella (Red Hat) reiterated a previous question about the availability of machines for contributors, specifically mentioning students from the University of Pisa who lack hardware.
  * Jörg Rödel stated he hasn't made progress on this but will re-raise it.
  * The main challenge is finding the right person internally to facilitate this.
  * He prefers to approach hardware vendors first before considering options like renting machines via the CCC (which would involve reimbursement, making him hesitant).

* Dionna Glaze (Google Cloud Platform) mentioned that GCP does not currently have SNP bare metal support to offer for this purpose but will take the request back to her team.
* Jörg Rödel will also continue to explore options.

### TDISP Roadmap

* Dionna Glaze asked if user space or Linux is expected for TDISP device management.
* Jörg Rödel noted that some parts must happen within the SVSM (kernel or user mode is unclear). For AMD, it involves communication with the security processor only from VMPL0, requiring SVSM involvement.
* James stated that Dan Williams seems to imagine mostly a pass-through. Microsoft is interested in terminating TDISP in the SVSM (as a Paravisor), but no code exists yet.
* Dionna Glaze asked if libspdm is all in C.
  * James confirmed it's C libraries, not difficult to use.
  * Jörg Rödel believed there is a Rust SPDM implementation, possibly a CCC project.
  * Tom Lendacky (AMD) clarified that SPDM might not be done within the SVSM, but rather initiated by a request to the Hypervisor, which then handles encrypted communication between the PSP and the device endpoint.
  * James countered that the guest ultimately decides whether to trust the device, which is effectively SPDM.
  * Tom Lendacky (AMD) agreed the guest would look at attestation reports.
  * James noted SPDM's difficulty due to physical function access.
  * Tom Lendacky (AMD) mentioned ongoing work by Alexey (not involving SVSM yet, as it's VMPL0 guest based) that would inform SVSM efforts.
  * James suggested an architecture where the guest pieces work identically in VMPL0 and SVSM guests, with SVSM shimming necessary parts due to VMPL differences.
  * James inquired about a recent CCC Kernel SIG meeting organized by Dan Williams to discuss IOMMUFD patches.
  * Jörg Rödel was unaware of the specific meeting, thinking Dan Williams had indicated such meetings were no longer needed.
  * James clarified it was a special meeting last Thursday to "knock heads together" and agree on a path forward for IOMMUFD patches due to their impact on TDISP implementations.
  * James will ask Dan Williams to post information about these meetings to the mailing list for better transparency.
