# Meeting Minutes: SVSM Development Call (August 14th, 2024)

## Attendees:

Adam Dunlap, Diego Gonzalez Villalobos, Dionna Glaze, Joerg Roedel, Jon Lange, Oliver Steffen, Peter Fang, ramakrishna gali, Sabin Râpan, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Joerg Roedel's Update
* Resolved stack unwinder issues and is investigating a crash related to user mode task exit.
* Working on improving APIs around interrupt enablement to support TD partitioning.
* Collaborating with Jon Lange on interrupt handling and TPR integration.

### Jon Lange's Update
* Addressed Roy's feedback on stage2 relocation PR.
* Seeking feedback on PR from Joerg and Peter.
* Discussing potential collaboration with Joerg on interrupt handling and TPR.

### Release Process Discussion
* Group discussed the potential benefits and challenges of implementing a release process.
* Agreed on the need for stable builds but are hesitant to commit to supported releases at this stage.
* Will explore versioning schemes and release criteria.

### Double-PValidate Issue
* Tom Dohrmann asked about progress on fixing double PValidate issues.
* Joerg Roedel outlined plans to remove direct-map and introduce a tracking data structure to fix it.
* Jon Lange highlighted the need for dynamic heap sizing in the SVSM to accommodate memory tracking.

### Other Topics
* Vijay Dhanraj inquired about the status of restricted injection protocol and potential plans for platform-specific implementations.
* Ramakrishna gali raised questions about measurement discrepancies between different tools and PCR register behavior in different boot modes.
