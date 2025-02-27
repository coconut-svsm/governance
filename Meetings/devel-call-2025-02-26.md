# Meeting Minutes: SVSM Development Call (February 26th, 2025)

## Attendees:

Adam Dunlap, Dionna Glaze, Joerg Roedel, Melody Wang, Oliver Steffen, Stefano Garzarella, Jon Lange, Geoffrey Ndu, Tom Lendacky, Cláudio Carvalho, Peter Fang, Vasant Karasulli

## Topics:

### SVSM Bus Discussion:

* The meeting started with a discussion about the SVSM bus for Linux.
* The interface to the architecture still needs to be defined.

### VTPM Driver Issue:

* Stefano Garzarella reported an issue with the VTPM driver on Linux 6.14-rc4 related to KVM.
* He plans to open an issue with more details and test without his changes.

### MADT-PR Update:

* Jon Lange updated a pull request (PR) related to MADT parsing, which had a mistake in generating the IGVM file.
* Joerg Roedel was testing it and will continue to do so.
* QEMU Implementation: Joerg Roedel and Jon Lange discussed the possibility of implementing MADT via IGVM in QEMU.
* Jon Lange mentioned that Adam had done it in their VMM, suggesting it might not be too difficult.

### Timer Issues:

* There was a discussion about timer issues, possibly related to the hypervisor's timer infrastructure and ACPI tables.
* Joerg Roedel shared his past experience with similar issues.

### CoCo Session at Linaro Connect:

* The proposal to organize a session for the COCONUT community at Linaro Connect didn't receive enough feedback and will be postponed to next year.
* KVM Forum: The KVM forum in Milan in September was suggested as a good opportunity to organize a gathering of the COCONUT community.

### vTPM Service Manifest Thread:

* The discussion about the VTPM service manifest thread and the byte order issue continued, with concerns about compatibility with existing Linux versions.

### Native Platform PR:

* Joerg Roedel announced the merging of the native platform PR, which allows running SVSM on non-confidential computing machines.

### SMAP, SMEP, and Shadow Stacks:

* The meeting participants discussed whether to require or dynamically detect SMAP, SMEP, and shadow stacks.
* The decision was to require them on confidential builds and autodetect on native environments.

### CI and Testing in SVSM:

* The participants talked about including native platform support in the launch script, writing tests for the native platform, and integrating with the CI.
* Requires IGVM support in the QEMU available in CI.

### vTPM Protocol and Attestation:

* There was a discussion about the VTPM protocol, attestation service, and the need for a new protocol.

### Naming Maintainers:

* The idea of naming maintainers for certain areas was raised and will be formalized.

### Soundness Issues in PerCPU

* Jon Lange mentioned finding and fixing a soundness issue in per-CPU areas related to race conditions during multiprocessor startup.
