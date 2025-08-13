# Meeting Minutes: SVSM Development Call (August 13th, 2025)

## Topics:

### Old Business

* Jörg Rödel and Peter Fang: Peter thanked Jörg for his help in debugging issues with OVMF IGVM memory map support.
* Jörg mentioned the problem seems to be in OVMF but he hasn't located the exact cause yet. He committed to helping Peter debug it further.

### Project Updates

* SVSM Project Release:
  * Jörg mentioned a recent project release went smoothly.
  * He thanked everyone involved in the release for their work, especially those who continued working over the summer.
  * Work has already started on the next release.

### Open Issues for Next Release

* Jörg highlighted two specific issues for the next release:
  * Release Crate Issue: The build.rs script in the release crate doesn't run every time, which prevents the correct release string from being generated. This requires a fix in the build tool.
  * Attest Feature: The "attest" feature can currently only be built using the Makefile, not the build system. Enabling it via the build recipe breaks the build. This needs to be fixed.

### Other Business

* Jörg Rödel's Work: Jörg mentioned he is currently busy with work outside the core SVSM project, specifically with implementing Planes support in QEMU." This means his activity on the SVSM project itself has been limited.
* Discussion: Jörg opened the floor for questions, updates, or other topics. No one had any questions or updates to share.
