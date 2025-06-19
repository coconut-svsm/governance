# Meeting Minutes: SVSM Development Call (June 18th, 2025)

## Topics:

### PR #609 – Hypervisor-Specific Field in IGVM Parameters

* PR proposes a hypervisor field in IGVM parameters to clarify firmware config interface presence.
* Jon Lange prefers feature-based detection over hypervisor-specific logic.
* Adam Dunlap and Jon Lange agree to rework the PR to rely on feature flags instead.
* Action: Adam to collaborate with Jacob to revise and rebase the PR.

### PR #721 – VTPM Support and TPM Template Initialization

* PR adds TPM support logic, enabling initialization of Google-specific TPM templates.
* Discussion centered around avoiding compile-time configuration in favor of runtime customization.
* Jon Lange proposed using a dynamic model where TPM code is loaded from an attested file system.
* Dionna Glaze highlighted technical challenges with Rust's type system and dynamic trait objects.
* James Bottomley questioned whether the TPM provisioning logic must reside in SVSM or could be shifted to user space.
* Jon Lange explained TPM provisioning must happen early and be ready before the guest OS boots.
* Dionna explained this is part of a “manufacturing step” for EK certificate provisioning by the VMM.
* Future Maintenance and Transition:
  * Dionna announced moving to a new role
  * Concerns raised about long-term maintainability if Dionna departs without a handover plan.
  * Adam Dunlap will assume responsibility for TPM-related code.
* Standardization & Portability Concerns
  * Portability between clouds (Google, Azure, AWS) discussed.
  * Jon stressed that each cloud will have its own TPM provisioning approach; SVSM portability may require future standardization.
  * A potential SIG (Special Interest Group) for defining virtualized TPM device behavior was mentioned.
* Google vs. Standard TPM Templates
  * The Google EK signing template differs in certain fields like authValue, and lacks NV index policy.
  * General agreement that some parts of the template (like EK signing) may be useful beyond Google.
  * Discussion about working with TCG to standardize such templates.
