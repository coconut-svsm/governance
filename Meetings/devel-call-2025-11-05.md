# Meeting Minutes: SVSM Development Call (November 5th, 2025)

## Topics:

### Report from Technical Steering Committee (TSC) Meeting

* **Policy PR & Code Owners**
  * The policy Pull Request (PR) has been merged.
  * The process of adding `CODEOWNERS` files has begun, starting with the SVSM repository and continuing for other non-downstream repositories.
* **Google Summer of Code (GSoC)**
  * The QEMU project is willing to take the SVSM project under its umbrella for GSoC.
  * Project ideas need to be factored out from the updated development plan.
  * Need to find mentors for each project before submitting the projects to QEMU (deadline is around early February).
* **COCONUT-SVSM Perception**
  * Discussion was held on the perception of COCONUT-SVSM as a minimal Rust kernel runtime, noting that it supports three usage models: SVSM mode, paravisor mode, and the Service-VM mode.
  * Ongoing discussion.
  * Update documentation to clarify that the COCONUT project is not solely an SVSM project.
* **Cocoon-FS PR Progress**
  * A plan was discussed for progressing the large CocoonFS PR.
  * Stefano and Oliver will port their existing full disk encryption with TPM disk unlock demo to use CocoonFS for storage as a proof-of-concept.
  * A design document for the storage format will be reviewed. Cryptographic peer-review is welcome but not a blocker. Nicolai Stange has pending renames from review comments.
* **Formal Verification**
  * Jörg Rödel confirmed two open issues in formal verification, one specifically around the verifier lacking support for a feature like "raw borrows" which currently breaks verification for Cocoon SVSM.
  * Ziqiao Zhou is aware of the issue.
  * Ziqiao Zhou will continue working on a fix for the formal verification issue.
* **Other PRs**
  * The IGVM memory map PR from Peter was reviewed and merged.

### SVSM Busy Error Handling

* Adam Dunlap raised an issue where SVSM panics when the hypervisor throttles guest requests and returns a "busy" error.
* A clean return of "busy" to the guest needs to be checked against an existing code comment about reusing IDs.
* Adam Dunlap will open a GitHub issue and a PR with a proposed fix to ensure no IDs are reused.

### Fallible Allocator Support

* Jörg Rödel clarified that the project will *not* wait for upstream Rust's allocator API due to observed upstream resistance.
* Carlos López and Vaishali Thakkar will work together to develop a proposal on how to move forward with the fallible allocator project.

### VSOCK and Attestation

* Discussion on the VSOCK PR mergeability, noting the need for a device tree for SVSM dynamic device detection.
* Stefano Garzarella suggested implementing the VSOCK feature for attestation alongside the existing serial port method for a default scenario, noting VSOCK's port listening check is sufficient for attestation presence detection.
* Question was raised whether VSOCK PR can be merged without SVSM supporting device tree enumeration.
* Jörg Rödel will consider if the VSOCK PR should be merged now to move attestation over to it.

### User Space Support

* User space is functional (user mode, syscalls, console printing work), but is missing a heap allocator and user mode threading support.
* An internal Microsoft project (OpenHCL) uses a Linux kernel and might have specific needs for SVSM adoption. The SVSM user space was not intended for full POSIX compatibility.
* Ziqiao Zhou will provide a list of needed syscalls and features from her colleague's project to help prioritize development work.
