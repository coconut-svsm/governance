# Meeting Minutes: SVSM Development Call (February 19th, 2025)

## Attendees:

Cláudio Carvalho, Dionna Glaze, Geoffrey Ndu, James Bottomley, Joerg Roedel, Nicolai Stange, Oliver Steffen, Peter Fang, Vasant Karasulli, Ziqiao Zhou

## Topics:

### PR Review

* Joerg Roedel reviewed and merged several PRs
* Reviewed the native platform support for QEMU and Tyler's PR.
* He requested more documentation on the proxy usage in Tyler's PR.
* Geoffrey Ndu inquired about PR 541 (vTPM Service Attestation).
* Cláudio Carvalho agreed to review again.

### Kernel Patch Status

* Cláudio Carvalho asked about kernel patches for the SVSM and whether an upstream kernel works.
* Joerg Roedel confirmed that booting works with a stock kernel (6.13)
* vTPM patches are still in progress.

### SVSM to Guest Communication Discussion

* Dionna Glaze asked about including the vTPM before the upstream driver is available.
* James Bottomley clarified that it's already in the SVSM build.
* Faux Bus Patch:
  * Dionna discussed a patch from Greg regarding platform drivers and virtual devices.
  * James Bottomley explained the context of Greg's comment and the abuse of platform devices.
  * They explored the idea of creating a faux bus or using an SVSM specific bus.
* SVSM Bus in Linux:
  * The participants discussed the possibility of defining an SVSM bus to enumerate more devices and handle interrupts for use cases like live migration.
  * They considered using Greg's patch set as a model but decided to create their own bus.
* James Bottomley will investigate Greg's patches and continue discussion next week.

### Early Back Traces

* Peter Fang introduced a PR to improve stack traces in the unwinder.
* Joerg Roedel acknowledged the PR and agreed it would be useful, also in Stage2.
* Still need an in-depth review.

### Rust Standard Library Support

* Joerg Roedel discussed the Rust standard library support for SVSM user space.
* They identified the need for a monotonic timer source (possibly Secure TSC) and discussed whether timer interrupts are necessary.
* Discussion will continue in the SVSM call soon.
