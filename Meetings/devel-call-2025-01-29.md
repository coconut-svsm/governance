# Meeting Minutes: SVSM Development Call (January 29th, 2025)

## Attendees:

Adam Dunlap, Cláudio Carvalho, Dionna Glaze, Hajira Zaman, Joerg Roedel, Jon Lange, Nicolai Stange, Peter Fang, Tom Lendacky, Vasant Karasulli

## Topics:

### GitHub Organization Membership:

* Joerg Roedel encouraged attendees to become members of the COCONUT-SVSM organization on GitHub to facilitate PR assignments, issue management, and code review requests.

### Doc Website Generation Workflow Failure:
        
* Joerg Roedel reported a failing doc website generation workflow on GitHub, possibly related to recent TPM changes.
* Cláudio Carvalho offered to investigate the issue with Stefano, who made the recent changes.

### Undefined Behavior in TPM:
        
* Jon Lange raised concerns about a PR addressing undefined behavior in the TPM by revoking guest access to a page while the TPM is processing.
* Participants discussed alternative solutions, including using atomics or creating a local copy of the guest data.
* Cláudio Carvalho will explore implementing safety without requiring permission changes.

### SMP Startup and TLB Flush:

* Jon Lange noted that TLB flush requires an IPI for remote processors, which requires interrupt support for the L1, currently unavailable.
* Peter Fang acknowledged the issue and will investigate further.
* Jon Lange suggested that TDP might be limited to single-proc until multi-privilege level interrupt support is added to KVM.

### Moving Main Request Processing Loop to a Separate Task:
        
* Jon Lange is working on a change to move the main request processing loop into a separate task, making it optional based on the platform.
* This change will enable the init task to shut down if request processing is not performed and allow TDP to boot to idle on TD partitioning.
    
### VE Handling and CPUID:

* Peter Fang inquired about tackling VE handling and CPUID.
* Jon Lange suggested adding a skeleton VE handler for CPUID and potentially for future MSR and IOIO handling.

### Scaling Memory Demands for SVSM:

* Jon Lange discussed Adam Dunlap's change enabling the hypervisor to predict SVSM private memory needs based on guest memory.
* Participants explored modifying OVMF to exclude SVSM memory from the UEFI memory map based on the secrets page.
* Dionna Glaze and Adam Dunlap will investigate this approach.
* Alternative approach: IGVM Memory Map Consumption on SNP:
  * Joerg Roedel expressed interest in using the IGVM memory map approach on SNP for unification across architectures.
  * Jon Lange agreed but noted that SVSM's existence might delay immediate implementation.
