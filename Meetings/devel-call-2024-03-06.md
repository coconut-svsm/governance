# Meeting Minutes: SVSM Development Call (March 6, 2024)

## Attendees:

Adam Dunlap, Carlos López, Cláudio Carvalho, Dionna Glaze, Eddie Dong, Foo Fighters, Huibo Wang, Joerg Roedel, Nicolai Stange, Oliver Steffen, Roy Hopkins, Thomas Leroy, Vasant Karasulli, Vijay dhanraj

## Topics:

### Updates:
* Joerg Roedel updated the Linux and qemu branches in the COCONUT SVSM project.
* Joerg Roedel will merge the meeting minutes from the past two meetings - no objections raised.
* Joerg Roedel invited everyone to attend the C3 conference, which will feature a session on COCONUT.
* No meeting next meeting because of conflict with the C3 conference.

### Persistent Storage for COCONUT:
* Oliver Steffen is working on persistent storage for COCONUT using the QEMU PFlash device.
* Nicolai Stange is working on an encryption and integrity layer for the storage.
* Discussion points:
  * Replay protection for the entire storage device is difficult to achieve.
  * Using a file system layer on top of the block level is desirable in the long term.
  * Different approaches for handling untrusted storage and trusted storage were discussed.
  * Early attestation using KBS was proposed to securely obtain keys for persistent storage.
* **Action Item**: Oliver Steffen will submit his work in stages for review, starting with the block layer.
* Attestation and Replay Protection: Dionna Glaze emphasized the need for attested measurements and the complexity of achieving replay protection, citing the dbx bootkit CVE as an example.
    
### Governance Repository:
* Dionna Glaze mentioned the open-source scorecard tool and suggested using it to evaluate the project's health.
* Joerg Roedel will investigate branch protection rules and the open-source scorecard.
    
### IGVM vs. OVF:
* Dionna Glaze inquired about the differences between IGVM and OVF, and if
  anyone had knowledge about them. She shared a link to a relevant discussion on [Hacker News](https://news.ycombinator.com/item?id=39005308).
* Governance: Dionna Glaze raised concerns about governance and suggested enabling specific settings using the [OpenSSF Scorecard tool](https://securityscorecards.dev/).
