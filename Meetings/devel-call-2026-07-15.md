# Meeting Minutes: SVSM Development Call (July 15th, 2026)

## Topics:

### TSC Meeting Update

* **Jörg Away for Two Weeks:** Stefano chaired the call and said Jörg was on vacation for the current and following week.
* **Nightly Toolchain Warnings Discussed:** Stefano said the TSC discussed how to handle warnings that appear when tests are run with the nightly Rust toolchain while the project still uses a stable toolchain for builds.
* **Nightly-Specific `allow`s May Be Avoided:** One example was the CPUID API being treated differently between nightly and the stable toolchain in use. The tentative preference was to tolerate some nightly warnings rather than pollute the code with `allow` attributes that might later be forgotten.
* **IGVM Optional Parameters Need Better Support:** Jon updated the TSC on IGVM optional parameters. QEMU already supports them, but support in the Rust crate is less complete. Stefano said Microsoft is expected to propose improvements in the coming weeks.
* **User-Space PRs Waiting for Jörg:** The TSC reviewed open PRs and decided to wait for Jörg's return before merging user-space related work where he had additional design input.
* **CPUID PR Follow-Up Ongoing:** The TSC discussed Tanish's CPUID PR, with Carlos helping review the approach.
* **TOML Formatting in CI Still Open:** Oliver opened a PR for TOML formatting, but the formatter takes a long time to build. Downloading a prebuilt binary was discussed, but previous security concerns led the project to remove binary downloads from CI.

### TOML Formatter and CI Tooling

* **Trusted Binary Source Question Raised:** James asked whether the security warning was specifically about untrusted prebuilt binaries and whether a trusted source for the TOML formatter exists.
* **Distribution Package Not Available:** Stefano said the TSC had looked for a package in the distribution used by CI, which would have been a more trusted source, but did not find one.
* **Cargo Install Still Has Trust Questions:** The formatter can be installed through Cargo, and a faster Cargo installation path may exist, but the group was not sure that this resolves the trust concern.
* **GitHub Cache Reuse Suggested:** Stefano suggested building the tool once and reusing it through GitHub caches, similar to existing approaches for verification tooling and QEMU.
* **Dedicated CI Container Considered:** Oliver suggested maintaining a project container image with the Rust toolchain and required tools preinstalled. Stefano agreed this could save setup time, while noting it would add maintenance work.
* **Tracking Issue Suggested:** Stefano suggested opening an issue to track the CI tooling options.

### Rust Toolchain Update

* **Rust 1.94 Update Planned:** Stefano said Jon is working on updating the Rust toolchain to 1.94.
* **Downstream Compatibility Checked:** Stefano asked whether downstream packagers, including Fedora and Google, expected problems with Rust 1.94.
* **Fedora Should Be Fine:** Luigi said Fedora should be fine because its latest Rust version is 1.96.

### CPUID PR Design

* **PR 1137 Discussed:** Tanish asked Carlos about the design direction for CPUID PR 1137, specifically whether CPUID values could be cached on first use without keeping the current macro-based approach.
* **Current Code Already Caches on First Access:** Carlos said the existing implementation already caches CPUID data the first time a feature is queried. The macro generates the table used to store and index those cached values.
* **Static Table Preferred Over Dynamic Allocation:** Carlos said a dynamically expanding table would require allocation and resizing, which may not be available when CPUID is queried early during boot.
* **Lookup Efficiency Matters:** Carlos also noted that a statically generated table allows direct indexing by feature, while a resizable list would likely require scanning or additional lookup infrastructure.
* **Duplicate Mapping Concern Remains:** Tanish said one concern with the macro approach is the two-level mapping between CPUID data, feature constants, and leaf/subleaf values.
* **Further Discussion Planned Offline:** Because of audio problems, Carlos suggested continuing the discussion offline and said he could join the follow-up meeting on Friday with Tanish and Luigi.
