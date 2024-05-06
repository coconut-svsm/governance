# Meeting Minutes: SVSM Development Call (April 24th, 2024)

## Attendees:

Carlos López, Cláudio Carvalho, Dionna Glaze, Eddie Dong, Ernestine Anderson, Jacob Xu, James Bottomley, Joerg Roedel (Chair), Jon Lange, Oliver Steffen, Peter Fang, Roy Hopkins, Tom Lendacky, Vijay dhanraj

## Topics:

### User Mode Merge
* Joerg Roedel proposed merging a PR related to user mode functionality.
* There were no objections, and the merge will proceed.

### GitHub Documentation
* Roy Hopkins presented a PR that automates publishing documentation to GitHub Pages.
* The PR was well-received and appears to be working as intended.

### Interrupt Support in SVSM
* Vijay dhanraj requested feedback on a PR regarding interrupt support for confidential VMs (issue #328).
* Jon Lange and Joerg Roedel discussed the need for a virtual APIC emulation and interrupt model definition.
* It was decided that Vijay and Jon would collaborate on this functionality.

### TD Partitioning with Qemu
* Peter Fang informed the group about a PR that adds support for TD partitioning in Qemu and Linux
* Joerg Roedel suggested merging the PRs as there is low risk due to no TDX support yet.

### Joining the COCONUT-SVSM Github Organization
* Cláudio Carvalho inquired about how to assign oneself to issues.
* Joerg Roedel offered to send another invitation to join the COCONUT-SVSM organization on GitHub.

### Linux Security Summit
* Joerg Roedel provided a brief update on his talk and hallway discussions regarding SVSM and TDX support

### Building the SVSM
* Cláudio Carvalho asked about the scope of the expected launch measurement printed at build time
* Roy Hopkins clarified that the measurement only includes the SVSM, OVMF firmware, and configuration within the IGVM file.

### Next Meeting
* Due to a public holiday, the next meeting will be in two weeks. An announcement will be sent via email.
