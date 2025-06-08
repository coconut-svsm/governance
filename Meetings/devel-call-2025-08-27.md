# Meeting Minutes: SVSM Development Call (August 27th, 2025)

## Topics:

### Richard Relph's Reboot Work:

* Richard needs a core protocol message code for a VMPL2 guest reboot at the SVSM level.
* He is currently using code 8, but needs an official code.
* Jörg suggested talking to Tom about this, as he owns the SVSM spec.
* The message code would trigger a reset of all vCPU and memory states at the SVSM level.
* Richard has a patch set for Linux to handle this, which he plans to send to the group for comments.
* He acknowledged that OVMF would also need to be updated to handle this new reset path, but has not yet worked on that.

### Jörg Rödel's Development Update:

* Jörg has been working on the build system and fixing the release string generation, and has a pull request open for this work.
* He plans to rework the pull request based on comments from Stefano.
* He mentioned that this work should be included in the next monthly development release, which is planned for the next two weeks.
