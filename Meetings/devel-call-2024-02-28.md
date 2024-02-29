# Meeting Minutes: SVSM Development Call (February 28, 2024)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Eddie Dong, Joerg Roedel, Jon Lange, Nicolai Stange, Oliver Steffen, Tom Lendacky, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Archiving Meeting Recordings:

* Joerg Roedel proposed uploading meeting recordings to YouTube for archival purposes.
* Dionna Glaze: Raised concerns about YouTube's archival suitability, suggesting CCC's storage as the primary option with YouTube as a secondary syndication channel.
* Decision: No objections to recording meetings, with recordings uploaded following the approach suggested by Dionna.
* Tom Lendacky asked to update the calendar invite to inform participants about recording and the chosen archival approach.

### TPM Driver Updates:

* Cláudio Carvalho presented updates on the TPM driver and its dependencies on kernel and host changes.
* Action Item: Joerg Roedel will update the Linux guest and host repositories once the TPM driver changes are merged.
* Discussion: The group debated the optimal strategy for handling untrusted entropy sources, with Dionna mentioning Nist sp800-90ar1 as a reference.

### Persisting Data in PFlash:

* Oliver Steffen initiated discussion on implementing persistency for the SVSM by writing to the P flash.
* Dionna Glaze: Suggested using sealing for persistence.
* Discussion:
** Dionna emphasized the importance of replay protection, mentioning hardware monotonic counters and escrow services as potential solutions.
** Jon Lange clarified the distinction between protecting individual files and the entire filesystem, suggesting that self-consistency within the filesystem might be achievable without a monotonic counter.
* Next Steps: The group agreed to explore design options for persistency, keeping in mind:
** Encryption layer for data protection.
** Block layer to allow for different backend options (P flash, remote storage, etc.).
** Replay protection mechanisms, considering the points raised in the discussion.
** Action Item: Joerg Roedel suggested adding this topic to a future meeting agenda for a more detailed discussion or discuss it via email.

### Pull Request Text and Labeling:

* Joerg Roedel inquired about the clarity of the text he has been adding to pull requests, including "wait for review" labels.
* Jon Lange: Clarified that modifying pull request labels likely requires write permissions, which might be limited to maintainers.

### Additional Notes:

* Dionna Glaze mentioned she is working on a transparent build of the binary for measurement transparency.

