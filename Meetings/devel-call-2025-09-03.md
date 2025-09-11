# Meeting Minutes: SVSM Development Call (September 3rd, 2025)

## Topics:

### Release timing of monthly COCONUT-SVSM development releases

* Proposal: shift from beginning of the month to end of the month.
* Reason: better alignment with monthly changes.
* Agreement in TSC.

### KVM Plane Support / Multi-VCPU Guest Issues

* Status update from Jörg Rödel.
* Current bugs:
  * IOAPIC routing with PCI devices (E1000 issue).
  * AP startup blocked in VMPL0 → hack workaround.
* Work ongoing in QEMU + kernel to handle plane recreation and IRQ routing.
* Device discovery improvements planned.
* Goal: patches as RFC on the mailing list in September.
* QEMU device plane property & IRQ routing
* New machine property: device-plane for default routing.
  * Override possible per device.
* Leads to clean separation of devices per plane.
* Helps replace SVSM hacks.
* Discussion on Plane Switch API & Interrupt Handling
  * Open questions with Paulo’s design changes in KVM.
  * Constraints: Plane 0 is always runnable, others may not be.
  * Need to clarify interrupt pending handling.
  * Plan to follow up after KVM Forum and start mailing list discussion.

### Pull Request workflow on GitHub (Richard Relph’s issue)

* Problem: PRs closed automatically after rebases on main.
* Same doc update submitted as PR #794, #795, #800.
* Advice: create topic branches instead of using main.
* Action: Jörg to review and merge PR.
