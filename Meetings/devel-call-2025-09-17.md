# Meeting Minutes: SVSM Development Call (September 17th, 2025)

## Topics:

### Update on Planes Work

* Jörg Rödel gave an update on the ongoing planes work. He mentioned that he and Paolo agree that having single VCPU objects per plane is a problem. Paolo is working on a new patch set, there's no timeline for when it will be posted.
* Jörg plans to post his own work next week, which is based on an older patch set. This will allow the downstream repositories for the kernel to be updated to a newer version.
* The current patch set still has a problem with a single vCPU object unsharing all vCPU state, which poses a risk if users deviate from the intended use.
* He wants to release the patches for testing before updating the branch.

### SVSM User Space Support

* Luigi Leonardi asked for an update on the SVSM user space support.
* Jörg responded that there is a plan, but no one is currently working on it because other tasks are a higher priority.
* Jörg offered to point Luigi to the next steps for this project, and Luigi accepted the offer to help.
* The next steps include finishing the user space allocator to allow user space to allocate resources, which will enable other features in the core library.

### Reboot Code Pull Request

* Richard Relph announced he has posted his reboot code for review.
* The first, larger commit is a run-length encoded bitmap data structure, which Richard described as "overwrought" and a learning exercise.
* The second, smaller commit adds the new core protocol command to reboot the guest and the necessary hooks into the existing SVSM.
* Richard has bumped the core protocol version to 2 for this feature.
* He mentioned that this is his first time doing open source work with Git, Linux, SVSM, and Rust and expects a lot of comments, asking for gentle feedback.

### Discussion on Virtio Crates

* Luigi Leonardi brought up the idea of forking the Virtio crates repository and using it as a Git submodule to make it easier to track upstream changes.
* Jörg recalled that the crates were imported to the SVSM codebase because only small parts were needed, and a lot of code was removed during the import.
* Oliver Steffen agreed that using a submodule would make it easier to follow the upstream repository and backport fixes.
* Luigi suggested forking the repository, applying necessary downstream patches (like removing unnecessary code), and then importing it as a submodule.
* Jörg expressed skepticism about the benefit of this approach, stating it might make rebasing and pushing changes upstream more difficult.
