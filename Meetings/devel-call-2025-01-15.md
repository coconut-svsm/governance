# Meeting Minutes: SVSM Development Call (January 15th, 2025)

## Attendees:

Adam Dunlap, Christopher Oo, Cláudio Carvalho, Dionna Glaze, Geoffrey Ndu, Huibo Wang, James Bottomley, Jean, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Peter Fang, Stefano Garzarella, Supreshna (HPE), Tom Lendacky, Tyler Fanelli, Vasant Karasulli

## Topics:

### Announcements

* No meeting on January 22nd, 2025, next meeting on January 29th.

### VTPM Persistence Presentation

* Geoffrey Ndu introduced a proposal for VTPM persistence, a different approach from current work.
* Jean presented a [security analysis](https://stringlytyped.github.io/publications/csvsm-proxy-security-analysis/)
  of the current proposal and outlined their new proposal. [Slides](Data/state-persistence-csvsm-slides.pdf)
  [Google Doc](https://docs.google.com/document/d/1DaTycUH0M2qU6lK0EF8d42g-e0CvBOD-3rxrk8lCea4/edit)
* Key points of the presentation:
  * Maintaining confidentiality and authentication of persisted keys.
  * Addressing the unique security challenges of CVMs.
  * Ensuring backward compatibility with existing applications.
  * Accommodating edge use cases with unreliable Internet connectivity.
* Discussion points:
  * The role of an attestation bridge in ensuring end-to-end secure channel.
  * The use of ephemeral vs. persistent EKs for attestation.
  * The importance of binding attestation to specific CVM instances.
  * The challenges of detecting rollback in CVM environments.
  * The potential use of a rolling hash and counter to detect rollback.
