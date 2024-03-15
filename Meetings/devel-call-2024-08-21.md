# Meeting Minutes: SVSM Development Call (August 21st, 2024)

## Attendees:

Diego Gonzalez Villalobos, Dionna Glaze, Huibo Wang, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Ramakrishna Gali (AMD), Roy Hopkins, Thomas Leroy, Tom Dohrmann, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Joerg Roedel's Update
* Submitted SVSM BoF session for the Plumbers conference.
  *  Noted that AV equipment is not needed.
* Worked on unblocking people who were waiting for merges.
* Implemented IRQ API to enable/disable interrupts for critical sections.
* Thanks to Tom Dohrmann for helpful reviews.
* Merged several PRs.
* Asked for help with debugging stack frame sizes in Rust.

### Logo Design for Coconut-SVSM
* Dionna Glaze presented several logo options.
* The community expressed preference for the shield design with a coconut tree.
* Funding for the logo will be discussed with the CCC.
* No decision yet, people have one more week to think about the logo design.

### Launch Measurement Test PR status
* Roy Hopkins asked about status of PR
* Joerg Roedel answered that it can not be merged as long as it breaks `make test-in-svsm`
* Discussion went to downgrading the failure to a warning for now and fixing the root causes for the measurement mismatches.

### Restricted Injection Implementation:
* Vijay Dhanraj discussed the design and potential issues with the global buffer approach.
* Tom Lendacky explained the reasons for using a per-vcpu buffer.
* The group agreed that the current approach is the most secure and efficient.
