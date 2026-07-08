# Meeting Minutes: SVSM Development Call (June 24th, 2026)

## Topics:

### TSC Meeting Update

* **Direct VMSA Alignment Improving:** Jörg said the direct VMSA upstream patch set was discussed by the TSC. Upstream feedback still requires extensive implementation changes, but there no longer appears to be fundamental disagreement that the feature is useful.
* **Planes Branches Updated:** Jörg said the downstream Linux and QEMU branches were updated to the KVM planes implementation on Thursday, June 18th.
* **Direct VMSA Issue Fixed Locally:** One reported issue was an inconsistency in the direct VMSA code. Jörg has fixed it locally and expects to push an `svsm-next` branch with that fix and possibly other updates for testing.
* **Restricted-Injection Issue Still Being Investigated:** A second issue may be related to event reinjection with restricted injection enabled. Stefano said the issue disappeared after Luigi updated the kernel on the affected machine, but he will continue helping debug which configuration triggered it.
* **Event Reinjection Logic Needs Cleanup:** Jörg said the current implementation still tries to reinject some events that should instead be retaken by the guest. With restricted injection, KVM-injected events such as `#HV` events are the exception that can be reinjected.
* **Exit-Code PR Discussed:** The TSC discussed the exit-code PR and concluded that exit codes should be optional for user tasks. Some API questions remain and the PR will be updated.
* **AI-Generated PR Process Reconfirmed:** Jörg said an AI-generated PR was discussed and will follow the same process as any other PR. If the change makes sense it can stay open and proceed; otherwise it can be closed.
* **`AGENTS.md` PR Nearing Merge:** Jörg said Carlos' PR adding an `AGENTS.md` file should hopefully be ready to merge soon, so people using AI tools can get better project-specific results.
* **Contributions to AI Guidance Welcome:** Stefano encouraged people to review and extend the AI guidance over time, since the file is only an initial version and the project is still learning what belongs there.
* **Release Checklist Documentation Planned:** Jörg said he was asked to add his release checklist to the repository. The release process may later include checking whether `AGENTS.md` remains up to date, potentially with example AI prompts stored in the repo.

### SharedBox Multi-Page DMA

* **SharedBox Multi-Page Support Discussed:** The TSC discussed the PR making SharedBox aware of multi-page buffers. The main concern was reliance on physically contiguous memory, since current heap allocations are guest-physically contiguous but that may change.
* **Need for Multi-Page DMA Unclear:** Jörg asked whether virtio really needs or benefits from multi-page DMA, or whether single-page DMA is sufficient.
* **Virtio Scatter-Gather Support Exists:** Oliver and Stefano said virtio supports scatter-gather style operation, and Linux uses it, but the current SVSM implementation details still need to be checked.
* **Optimization Can Wait:** Oliver said the current implementation breaks requests larger than one page into separate commands, which causes more VM exits than a scatter-gather command would. He did not think SVSM is hitting a performance ceiling, so the group agreed this can be optimized later.

### Log Buffer PR

* **Console Output Should Stay Enabled Initially:** Jörg said he tested Vasant's log-buffer PR and asked for one small change before merge: keep console output enabled for now.
* **Runtime Control Needed Later:** Jörg said disabling console output is still the goal, but the project should first have a way to dynamically enable or disable console output for debugging.
* **Observability Work Will Build on It:** Once the log-buffer PR is ready, the related observability work can continue.

### Page-Table PR and TLB Flushing

* **TLB Flush Handling Needs More Design:** Ziqiao said she is working through TLB flushing behavior in the page-table PR. Some page-table operations can let the caller flush, but `set_shared` and `set_encrypted` may split huge pages, which means the caller may not know whether a page-level or wider flush is needed.
* **Linux-Style Gather Approach Suggested:** Jörg suggested considering an approach similar to Linux's TLB gather logic, where code that modifies page tables records the address range or flush requirements and lets the caller decide how to flush.
* **Avoiding Duplicate Flushes Is a Goal:** Ziqiao said the current implementation can perform duplicate TLB flushes. Returning information about the affected range or page size could avoid unnecessary flushes.
* **GHCB Drop Path May Miss a Flush:** Ziqiao noted that dropping a GHCB page appears to transition it from shared to private without an explicit TLB flush. Jörg agreed this should be correct in the module even if it may not currently be a practical runtime issue because most GHCBs are static.
* **Hypervisor Flush Behavior Is Not Enough:** Jörg noted that the hypervisor must flush because RMP state is cached in the TLB, but Ziqiao said guest code should not rely solely on hypervisor behavior for correctness.
* **Shared Interface Should Not Freeze Too Early:** Jörg said he wants to avoid a situation where the page-table crate API becomes hard to change because multiple projects, such as COCONUT-SVSM and Litebox, start depending on it before the interface is right.
* **Litetbox Requirements Are Similar:** Ziqiao said Litebox currently has relatively simple page-table needs, mostly map, unmap, and split operations, and she is involved enough to ensure the proposed interface works for both projects.

### Page-Table Volatile Access

* **Active Page Tables May Need Volatile Access:** Ziqiao said page-table memory access does not fully fit Rust's normal memory model once a page table is installed, so active page-table entries should likely use volatile reads and writes rather than ordinary references.
* **Tracking Active State Is Hard:** Jörg and Ziqiao discussed whether software should track whether a page table is active. Ziqiao said once a page table is installed or loaded into CR3, the current code loses clear tracking of whether it remains active.
* **Metadata Beside Page Tables Considered:** Jörg suggested that page-table roots could be wrapped with metadata indicating whether they are active, updated by the task-switch code. He also noted the code may need to know whether a page table is active on the current CPU.
* **Conservative Volatile Access May Be Simpler:** Ziqiao suggested treating page tables as possibly active and using volatile access conservatively. This would be correct for installed page tables and likely harmless for uninstalled ones.
* **Discussion Will Continue in the PR:** Jörg said he needs to think more about the best design. Ziqiao has related changes and the discussion will continue on the PR.
