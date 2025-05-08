# Meeting Minutes: SVSM Development Call (May 7th, 2025)

## Topics:

### Announcements:

* Jörg Rödel announced his upcoming move to AMD in June, which necessitates the migration of the meeting platform from Google Meet to the Linux Foundation Zoom Platform.
* The move to the Linux Foundation Zoom Platform will allow for more flexible meeting management.
* Jörg Rödel will have more time to focus on the project at AMD.
* A technical steering committee is being formed for the project.

### Discussion:

#### Impact of Jörg Rödel's move to AMD:

* Dionna Glaze raised concerns about the impact on support for ARM and TDX.
* Jörg Rödel clarified that the project will maintain its commitment to running on all platforms and hypervisors.

#### SVSM Specification Governance:

* Dionna Glaze inquired about AMD's plans for delegating governance of the SVSM specifications.
* James Bottomley suggested moving the spec into a repository under COCONUT-SVSM to facilitate development.

### Build Failures:

* Jörg Rödel reported a build failure with the user init.
* Oliver Steffen mentioned other build issues with release builds.
* Jörg Rödel proposed addressing the user init issue separately from the release build issues.
* Jon Lange offered to investigate refactoring Stage 2 to resolve release build problems.

### KVM Forum Call for Proposals:

* Stefano Garzarella announced the [call for proposals for the KVM Forum](https://lore.kernel.org/qemu-devel/905e09ae-df13-458e-9eb2-90ff455d1ee4@gnu.org/).
* The deadline for submissions is in one month.

### VM Planes:

* Dionna Glaze inquired about the status of VM Planes in KVM.
* Jörg Rödel provided an update on the infrastructure patch set and ongoing work.

### VirtIO Block Pull Requests:

* Oliver Steffen requested comments on the VirtIO Block pull requests.
* Stefano Garzarella agreed to review them.
* Jörg Rödel emphasized the importance of updating QEMU for testing SVSM.
* Dionna Glaze sought clarification on testing virtual device driver support.

### UEFI Variables in OVMF:

* Dionna Glaze raised the topic of having UEFI variables in OVMF communicate with SVSM directly.
* Stefano Garzarella mentioned that Gerd Hoffman is exploring exposing the UEFI variable store through the FWCFG interface in QEMU.
* [OVMF discussion](https://github.com/tianocore/edk2/issues/11044#issuecomment-2857333700).

### Formal Verification PR:

* Ziqiao Zhou provided an update on the large verification PR.
* Jörg Rödel is reviewing the PR and will provide comments.
