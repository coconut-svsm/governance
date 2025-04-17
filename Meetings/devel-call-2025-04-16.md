# Meeting Minutes: SVSM Development Call (April 16th, 2025)

## Topics:

### Announcements:

* Next week's meeting (April 23) is cancelled due to Joerg's vacation. The next meeting will be on April 30.
* Reminder about the new mailing list on lists.linux.dev. Participants were encouraged to subscribe. The old mailing list will be phased out.
* Project new has a room on matrix.org for real-time discussions. The link was shared on the mailing list.
* Meetings will be moved from Joerg's SUSE account to CCC infrastructure, likely using Zoom for transcription purposes. This change will occur in May.
* Meeting scheduling may shift to US time zones due to the CCC calendar.

### CI Hardware:

* Discussions with TAC chair of Confidential Computing Consortium (CCC) about acquiring CI hardware.
* CCC prefers vendors to be found and costs expensed, rather than self-hosting.
* Physical machines are required, not virtual machines.
* Need to investigate vendors for renting CI and development machines.
* Stefano will check with Kata-Containers project about their CI setup.
* Alternative is to ask hardware vendors to provide machines in their labs.
* Need to determine how to set up GitHub CI to use external machines. Stefano and Oliver offered to help.

### VirtIO-Block Pull Request:

* Oliver's VirtIO-block pull request was discussed.
* Reviewers were encouraged to provide feedback.
* Discussion about including the VirtIO drivers crate and preserving patches in the git history. It was decided to import the full crate first and then add patches.

### Stack Issue and Attestation PR:

* Discussion about the stack issue with the attestation PR and Nikolai's recent email with better crypto code.
* James suggested the stack issue might be due to the Rust crypto libraries being used.
* Discussion about crypto libraries in the SVSM, including OpenSSL, BoringSSL, and the need for FIPS certification.
* Discussion about using the TPM internal libraries and the need for a higher-level interface.
* Stefano will open an issue to continue the crypto discussion.
* Consensus to focus on feature progress and address crypto architecture later.
* Agreement to avoid introducing new random Rust crypto and try to use OpenSSL for now.

### IPI Driver Change:

* Joerg's APIC driver change was merged.
* Jon rebased his use of IPIs PR on top of it and it's ready for testing.
* Peter will rework his TDX IPI PR.
* Joerg fixed and merged the HyperV-TDP PR.

### SEV-SNP Emulation in QEMU:

* Stefano discussed the idea of a student thesis on emulating SEV-SNP architecture in QEMU.
* Feasibility was discussed, with concerns about the timeframe.
* Suggestion to limit the scope to SEV-ES emulation instead of full SNP.
* Need to emulate a PSP.
* Cláudio suggested asking Tom Lendacky for insights and concerns. Stefano will email Tom and CC the mailing list.

### Attestation Protocol and Crypto Hash:

* Dionna rebased the attestation protocol PR, but CI is failing.
* Proposal to add a crypto hash type (start, update, end) to unblock the merge.
* Joerg will do testing and another round of merges on Thursday.
