# Meeting Minutes: SVSM Development Call (March 27, 2024)

## Attendees:

Carlos López, Cláudio Carvalho, David Altobelli, Dionna Glaze, Eddie Dong, Huibo Wang, Jacob Xu, James Bottomley, Joerg Roedel, Oliver Steffen, Roy Hopkins, Stefano Garzarella, Thomas Leroy, Tom Lendacky, Vijay dhanraj

## Topics:

### vTPM Merge Status:

* Joerg Roedel noted that Cláudio Carvalho had addressed review comments and
  fixed a compile issue.
* Open conversations remain and need to be resolved before merging.
* Dionna Glaze raised a concern about the inclusion of OpenSSL from the
  vendor's package repository instead of the SVSM source code. This would create
  an indirect dependency that wouldn't be suitable for offline environments.
* The discussion revolved around the best approach for handling dependencies
  during packaging for various distributions.
* It was agreed that a decision on dependency management would be deferred.

### Vendored Dependencies:

* Joerg Roedel expressed concerns about Dionna Glaze's pull request (PR) that
  proposed including all dependencies in the SVSM repository.
* Dionna Glaze explained the benefits of this approach for maintaining a
  transparent build process and eliminating the need to modify source code. She
  envisions a build script using Google packaging options to select specific
  crypto implementations and features without altering source code. The build
  container would be self-contained and not require network access during the
  build process.
* Joerg Roedel clarified that the build container would include a vendor
  dependency repository along with the source code.
* James Bottomley compared this approach to the OBS (Open Build Service)
  method, suggesting that if it works for OBS, it should work for SVSM as well.
* It was agreed to explore the possibility of a script in the SVSM repository
  which prepares the source for offline build.

### Fallible Allocator

* Background: Carlos implemented a PR for fallible allocators, which is needed.
* The Rust for Linux people are using a fork of the upstream allocator with modifications.
* Upstream allocator relies on unstable Rust features.
* Kernel people's allocator uses build flags that are not well documented
* Potential performance drawbacks of not using the upstream allocator.
* Possible Solutions:
  * Collaborate with the Rust for Linux people and upstream to get the needed features stabilized.
  * Use the allocator that the Rust for Linux people are using and provide feedback to upstream.
* **Action Items:**
  * Joerg will reach out to the Rust for Linux people again to discuss collaboration.

### PFlash Implementation

* Oliver Steffen implemented a P-Flash driver but it's slow due to VM exits.
* Investigate using virtio-mmio for storage device attachment.
* Explore using a pluggable back-end for storage devices.
* Share the P-Flash driver when ready

