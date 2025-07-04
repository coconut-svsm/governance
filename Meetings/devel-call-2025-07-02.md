# Meeting Minutes: SVSM Development Call (July 2nd, 2025)

## Topics:

### Hardware for CI 

* Donation and Hosting: Hardware vendors might donate systems, but hosting needs to be secured by the team. 
* Hosting Plan: The current plan involves approaching universities for hosting, with Oregon State University Open Source Lab (OSUOSL) being a preferred option due to its existing project for open-source hardware hosting and its location in the US, simplifying shipping.

### Live Migration for Confidential VMs (SEV-SNP) 

* Current Status: Pankaj Gupta provided an update on the live migration efforts for confidential VMs, especially for SEV-SNP. It's currently a Proof of Concept (PoC) with some components developed, but not yet production-ready. 
* QEMU Integration: The live migration is initiated by QEMU, with command communication built between QEMU and SVSM.
* The plan is to convert QEMU migration threads to call into SVSM for packaging data to be sent to the destination. 
* Remaining Work: A significant part of the remaining work involves starting the guest at the destination site. 
* Community Collaboration: Community collaboration is desired for aspects like attestation and key sharing, which haven't seen much work yet. 
* Scalability: There's also a focus on scaling the process beyond a single VCPU for packaging, based on future experiments.
* PoC Sharing: Pankaj will share the PoC once basic live migration is functional. 
* TLS for Key Exchange: Discussion arose regarding using a TLS library for secure connection and a separate authentication step for key exchange between source and destination, rather than custom encryption. This approach would simplify FIPS certification. 
* Integration with Attestation: The integration of live migration with attestation is a future discussion point, to be tackled after establishing live migration support. 

### Validated Page Tracking

* Current Status: Richard Relph provided an update on reboot work in SVSM, stating it's mostly working and he's now focusing on validated page tracking. 
* Challenges: Jon Lange noted that validated page tracking makes the SVSM's memory allocation variable, requiring a contract with OVMF for memory awareness. 
* Proposed Solutions & Difficulties:
  * Teaching QEMU to determine SVSM's memory consumption, which would involve significant logic in QEMU and is not considered a robust long-term strategy. 
  * SVSM deciding its memory needs and informing OVMF. Peter Fang started exploring this, but it's not trivial and will take time to establish a good protocol for memory consumption and handoff. 
* Richard Relph's Approach: Richard plans to try approaches that don't require external memory management, hoping a reasonably sized static allocation within SVSM might suffice for his current test cases. Jon Lange expressed concern that this approach might quickly lead to memory exhaustion.

### IGVM Patches

* Roy Hopkins noted he will send out version 9 of the patches later this week.
* Adam asked whether non-IGVM boot is still supported
  * Agreement that no non-IGVM boot consumers are left and the code can be removed
  * QEMU IGVM patches do not provide MADT table to SVSM yet, FWCFG still needed for getting APIC-IDs
* Jon Lange mentioned he would likely have time to extract the non-IGVM code from the patches over the next few days. Adam Dunlap stated he had no strong feelings about doing it himself but was willing to help if Jon couldn't do it quickly enough.
