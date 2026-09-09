# Meeting Minutes: SVSM Development Call (September 2nd, 2026)

## Topics:

### TSC Meeting Update

* **TDX Support Remains on the Roadmap:** The TSC confirmed that TDX support is still planned, but the current team does not have enough bandwidth to work on it.
* **External Contributions Are Welcome:** Contributors or organizations interested in advancing TDX support are encouraged to help. The project would still like to support TDX in the future, but has no implementation schedule at present.
* **Page-Table Rework Is Progressing:** Carlos is removing the page-table code's dependency on the direct map. The TSC discussed the scope, approach, and possible follow-up work.
* **Page-Table PR Expected Soon:** Carlos expects to post a PR by the end of this week or during the following week, where the detailed design discussion can continue.
* **PR 1209 Needs a Transition Period:** The TSC noted that PR 1209 introduces breaking changes. The project will allow time for users to test the changes and transition to a newer QEMU/KVM version that supports them.
* **Observability Protocol Rename Still Open:** The TSC would like to replace the "Observability and Configuration Protocol" name and its OCP abbreviation, but did not select a new name. Discussion will continue.

