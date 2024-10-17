# Meeting Minutes: SVSM Development Call (October 16th, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Diego Gonzalez Villalobos, Dionna Glaze, Hajira Zaman, James Bottomley, Joerg Roedel, Mingshen Sun, Oliver Steffen, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Announcements

* Meeting Time Zone: The meeting is scheduled in European time zone. Please be mindful of daylight saving time changes.
* Microsoft Research Collaboration: Researchers from Microsoft are interested in applying formal verification of Rust code to the SVSM. They will be presenting their work and discussing integration possibilities in an upcoming meeting.

### OC3 Conference

* Submission: The deadline for submitting sessions to the OC3 conference in March 2024 is in December. The team will discuss potential submissions in future meetings.

### Rust Version Bump

* Decision: The team is generally fine with bumping the rust version.
* Verification Tool Compatibility: The verification tool may need to be updated to support the newer Rust versions. The team will discuss this with the researchers during their presentation.
* Next Steps: The team will wait for the next Rust release (1.82) and conduct testing to ensure compatibility. If there are no issues, they will update the Rust version in the following week.

### Deployment of SVSM in Cloud Environments

* Question: How to deploy SVSM in the cloud
* Cloud Provider Decision: Cloud providers need to decide whether to support SVSM.
* Experimental Feature: SVSM is currently an experimental feature and may not be immediately adopted by cloud providers.
* Timeline: The adoption of SVSM in cloud environments may take some time, depending on the development and release of necessary features.

### Root of Trust (TPM) Maturity

* VTPM Development: The VTPM is under development, with basic features currently available.
* Attestation Protocol: The attestation protocol for the VTPM is still being discussed, with potential differences between Intel and AMD implementations.

### TDX Enablement Progress

* Joerg Roedel asked whether all blockers for TD Partitioning support are resolved.
* Peter Fang: Blockers are resolved. The TDX enablement is progressing, working on updating the PR.

