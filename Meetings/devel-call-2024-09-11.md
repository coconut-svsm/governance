# Meeting Minutes: SVSM Development Call (September 11th, 2024)

## Attendees:

Adam Dunlap, Diego Gonzalez Villalobos, Dionna Glaze, Elena Reshetova, Huibo Wang, James Bottomley, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Roy Hopkins, Stefano Garzarella, Tom Dohrmann, Tom Lendacky, Vijay Dhanraj

## Topics:

### COCONUT-SVSM BoF at LPC
* The COCONUT-SVSM BoF was accepted for the next week's Linux Plumbers Conference.
* It is scheduled on Thursday at 5 PM.
* An email will be sent to the SVSM and KVM lists to invite people to the session.

### Shadow Stacks
* Tom Dohrmann is working on Shadow Stacks for SVSM and hopes to get a PR open this week.
* He is troubleshooting one last issue and then it should be reviewable.
* Joerg Roedel is curious to learn more about Shadow Stacks and review the PR.

### Early Attestation and Measurement Architecture Document
* Stefano Garzarella added a section to the document related to the rollback attack and clone attack.
  * Not completed yet, maybe discuss in the BoF.
* He also mentioned that Dionna updated the document with more details.

### System Calls
* Peter Fang gave an update on the system calls PR.
* They are working on getting a PR ready for the initial stuff.
* The PR will not include everything that they've done so far.

### `PageRef` Implementation
* Joerg Roedel discussed the improvements to the PageRef implementation done by Tom Dohrmann
* He mentioned that the read and write interface makes it more clear for the compiler that this is something different than rust data.
* Tom Dohrmann explained the intention behind the PR and agreed that the read and write interface is a good solution.

### Linux Plumbers Conference
* Peter Fang asked about the deadline for submitting slides and if the conference will be in-person only.
* Joerg Roedel responded that slides should be submitted by Thursday next week and that the SVSM BoF will be in-person, but there may be a way to join the BoF virtually using self-help AV equipment.

### GHCB Borrowing Mechanism
* The group discussed the issue of logging in exception handlers.
* They agreed that a more clever borrowing mechanism is needed to fix the double borrow issue for the GHCB with nested exceptions.
