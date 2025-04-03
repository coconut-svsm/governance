# Meeting Minutes: SVSM Development Call (March 26th, 2025)

## Attendees:

Joerg Roedel, Dionna Glaze, Adam Dunlap, Tom Lendacky, Stefano Garzarella, Oliver Steffen, Peter Fang, Ziqiao Zhou, Nicolai Stange, Jakub Růžička

## Topics:

### Opening and Announcements:

* Joerg Roedel welcomed attendees and noted it was the last week with the current time zone difference.
* Discussed attendance for the OC3 conference in Berlin. Dionna Glaze will present remotely, and Joerg Roedel will attend in person.

### PR Status:

#### [PR 259](https://github.com/coconut-svsm/svsm/pull/259) - Require SNP Restricted Injection:

* Joerg noted restricted injection is enabled in their development kernel but wanted to discuss requiring it in the SVSM.
* Adam (Google) reported concerns from Sean Christopherson about the KVM patch for restricted injection, preferring to keep it disabled.
* Discussion on SEV_FEATURES features, IGVM file, and VMSA.
* Tom Lendacky asked for Sean's reasons for disliking the patch.
* Adam explained the patch's limitations to VMPL0 and sketchy API with user space.
* Joerg mentioned the feature's relevance to multiple VMPLs and implementation in their development kernel.
* Adam confirmed Google is not planning to support restricted injection currently.
* **Decision**: Delay requiring restricted injection until upstreaming on the KVM side and broader hypervisor support.

####  [PR 528](https://github.com/coconut-svsm/svsm/pull/528) Attestation Driver and Proxy (with KBS Attestation):

* Discussion on increased stack usage in the pending PR.
* Stefano Garzarella acknowledged the issue and plans to investigate with Tyler, focusing on heap allocation and key generation.
* Joerg noted stack size impact on multi-CPU support.
* Stefano mentioned a potential feature flag that Joerg might have missed.
* Joerg to retest considering the feature flag.

#### [PR 541](https://github.com/coconut-svsm/svsm/pull/541) VTPM Service Attestation:

* Discussion on ongoing protocol discussions.
* Dionna Glaze is reworking the PR and encountering "invalid argument" errors.
* Dionna is trying to break the PR into smaller parts and needs a better way of reading and writing guest memory.
* Joerg mentioned existing mapping guard and guest pointer features.
* Dionna explained guest pointer limitations with variable-sized slices of bytes.
* Joerg to look into providing a variable-sized version of the guest pointer next week.
* Dionna needs the variable size for the selector, which can be large.
* Discussion on undefined behavior with TPM and Stefano's work on simplifying TPM code.
* Dionna needs an SVSM specification change for the manifest selector attribute.
* Dionna requested Tom Lendacky to review her branch on the mailing list.
* Dionna clarified her work in relation to Geoffrey's PR and will communicate with Geoffrey.
* Discussion on VTPM patches in EDK2 and SEV crashes. Stefano provided a link to a report.
* Tom Lendacky suggested separating base memory encrypt from enable/disable features.

#### [PR 635](https://github.com/coconut-svsm/svsm/pull/635) VirtIO Block Storage:

* Joerg stated the PR is mostly ready but discussed MMIO access routines.
* Oliver Steffen plans to add this to the SVSM platform and can do it now or in a follow-up.
* **Decision**: Oliver to add the MMIO access routines now.

#### [PR 622](https://github.com/coconut-svsm/svsm/pull/622) Early Stack Unwinding:

* Joerg reviewed Peter Fang's PR, requested a change, added the "update needed" tag.

### ACPI Issue:

* Discussion on the SVSM reading ACPI tables from firmware config and Linux issues.
* Tom Lendacky suggested a reset might be needed when reading ACPI tables.
* Joerg shared a past ACPI table issue related to QEMU regenerating tables.
* Stefano asked if Joerg still has the patch in his QEMU.
* Joerg confirmed he sees the issue and the patch was likely lost when switching to to IGVM.
* Joerg suggested injecting the MADT table via IGVM as a long-term solution.
* Adam mentioned the MADT being fed through IGVM, but QEMU might not support it.

### Formal Verification:

* Ziqiao Zhou reported the previous formal verification added to SVSM is broken due to code refactoring and is fixing it in a PR.
* Discussion on unifying annotations between pure spec mode and executable mode.
* Ziqiao is working on verification for the memory allocator and raised a question about freeing a compound page.
* Joerg suggested removing the feature of freeing a block of memory from any address and requiring freeing from its first address.
* Ziqiao will remove that part.
* Discussion on the SLAB allocator and similar issues.
* Joerg thanked Ziqiao for fixing the verification issues.

### CI Hardware:

* Oliver Steffen asked about getting hardware for CI testing.
* Joerg suggested talking to hardware vendors or the CCC.

### Google Summer of Code:

* Stefano mentioned updating the Google Summer of Code wiki page as students are already applying.
* Discussion on potential projects, including the CPUID feature handling.
* Joerg to write up the Google Summer of Code ideas in more detail.
* Stefano to send Joerg an email and add info to the QEMU wiki.
