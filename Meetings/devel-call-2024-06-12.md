# Meeting Minutes: SVSM Development Call (June 12th, 2024)

## Attendees:

Cláudio Carvalho, Dionna Glaze, Huibo Wang, James Bottomley, Joerg Roedel, Nicolai Stange, Peter Fang, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Introduction

* No meeting next week as Joerg Roedel will be at SUSECon
* Next meeting on June 26th, 2024

### TPM Locality for SVSM vTPM

* Cláudio Carvalho raised the question of using locality to reserve a secret for the SVSM unsealable only at the SVSM level.
* James Bottomley explained that localities are currently usable and the SVSM vTPM can use any locality. He suggested documenting this behavior and potentially using localities later.

### OVMF and Event Logs

* Cláudio Carvalho inquired about OVMF recording measurements in the PCRs and updating the event log in the SVSM.
* James Bottomley clarified that OVMF event logs are currently held in memory and not accessible by the SVSM at startup.
* Options discussed included:
  * OVMF adding event logs retrospectively after receiving measurements from the SVSM.
  * Developing a query protocol for OVMF to retrieve measurement information from the SVSM.
* Consensus leaned towards deferring development until a concrete use case arises.

### SVSM Measurements

* Joerg Roedel suggested measuring the machine configuration received from the hypervisor for integrity purposes.
* James Bottomley emphasized measuring only what the SVSM utilizes.
* The group discussed potential benefits and placement of measuring specific data like ACPI tables.

### PCR Banks

* Cláudio Carvalho asked about enabling specific PCR banks.
* James Bottomley suggested enabling SHA256 as a common choice and questioned the need for SHA384 due to its limited use in physical systems.
* SHA384 might make sense to have compatibility with TDX RTMRs.
* The group agreed on enabling SHA256 based on compatibility and common practice.

### Sycall ABI Document

* Joerg Roedel sent initial draft of System Call specification to SVSM mailing list.
* Review and feedback is requested.
* Broader discussion going to happen on mailing list and in next meeting.
