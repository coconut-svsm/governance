# Meeting Minutes: SVSM Development Call (August 28th, 2024)

## Attendees:

Adam Dunlap, Derek Miller, Diego Gonzalez Villalobos, Dionna Glaze, Elena Reshetova, Harvey Danger, Huibo Wang, Joerg Roedel, Nicolai Stange, Peter Fang, Stefano Garzarella, Tom Dohrmann, Vasant Karasulli, Vijay Dhanraj

## Topics:

### Project Logo

* The proposed logo was discussed and generally approved by the attendees.
* Joerg Roedel will start the process of transferring artwork copyrights and adopting it.
* The logo will be used on slides and the future website.

### Separate `igvmbuilder` from SVSM repository

* Adam Dunlap proposed separating the data structures of SVSM and `igvmbuilder`.
* Joerg Roedel suggested moving the `igvmbuilder` to a separate repository in the long term.
* A temporary solution of forking the data structures was discussed but rejected due to potential compatibility issues.
* Joerg Roedel will discuss with Roy about the changes needed to move the `igvmbuilder` out of the SVSM repository.

### Measurement Test PR

* Stefano Garzarella updated the PR with the suggested warning.
* The issue with the measurement test failing on certain setups was discussed.
* It was decided to keep the test as a warning for now until measurement becomes more stable.

### System Calls POC

* Peter Fang shared an update on the system calls POC.
* They are working on documentation and the object management framework.
* They plan to share the first version of the init process soon.

### Early Boot Attestation Document

* Joerg Roedel proposed discussing the document about early boot configuration in the next meeting.
* Dionna Glaze mentioned the need for a Port-io interface to register a shared page with the VMM for communication with the network proxy.
* Stefano Garzarella suggested using a serial port or a virtio device for communication.
* Document will be discussed in next meeting.

### Persistent Storage

* Stefano Garzarella provided an update on the persistent storage implementation.
* They have made progress on the block driver and are working on supporting the Microsoft TPM simulator.
* Plan is to make progress in the virtio-blk PR and get it merged.
* A more generic block driver interface can be added on-top of that.
