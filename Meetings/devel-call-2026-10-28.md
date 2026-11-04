# Meeting Minutes: SVSM Development Call (October 28th, 2026)

## Topics:

### TSC Meeting Update

* **Early Debug Logging Can Proceed:** The TSC agreed that Luigi's early debug logging PR can proceed in its current form. Jörg will review it and provide feedback. A future option to disable logging entirely, including the log buffer and turning log calls into no-ops, was discussed but is not a requirement for this PR.
* **Deadlock Detection Will Be a Debug Feature:** The TSC decided that same-CPU deadlock detection and related lock-debugging instrumentation should be used for debugging rather than enabled in production. The checks to implement and the strategy for extending them remain under discussion.
* **Address-Space Allocation Work Is on Hold:** The conflicting address-space allocation PRs, 1215 and 1221, are on hold until Jörg's per-CPU rework is complete. Three more PRs are needed for that rework; one is posted and two are still in development.

### Syscall Support and Musl User Space

* **SYSCALL Will Replace INT 0x80:** Mahmoud's PR switches to the `SYSCALL` instruction with a `#UD` workaround. He has addressed most of the feedback discussed so far and invited additional review. Jörg said the overall approach looks good but still needs an in-depth review.
* **Interrupt-Origin Checks Should Be Preserved:** The TSC wants to retain the code that distinguishes external interrupts from software interrupts, even though removing `INT 0x80` leaves it unused. Jörg explained that these checks are needed for security if software interrupts are introduced again. The code can be annotated as unused, and Jörg will leave a PR comment identifying what should remain. Mahmoud will revisit the cleanup commit.
* **Musl Support Is Being Upstreamed in Stages:** The syscall change is part of Mahmoud's work to run Linux-style user-space programs built against musl in SVSM. He has split the work into four or five PRs, with the first two submitted, and will post the rest after those merge. The intended result is a musl-linked Hello World program, with the missing syscalls added along the way.
* **A Development Branch Will Be Shared for Testing:** Mahmoud estimated that the broader work is 70–80% complete, with syscalls moved to Linux conventions, `exec` implemented, and two or three syscalls still missing. Jörg asked for a branch showing the combined result so he can inspect and test it. Mahmoud agreed to publish and share the work on his fork.
* **Instruction-Memory Race Was Discussed:** Mahmoud raised the possibility of user space changing the instruction bytes between a `#UD` exception and the handler reading them. Jörg explained that if the handler no longer finds `SYSCALL`, it treats the exception as a normal invalid-opcode event and kills the task. Both considered the race non-exploitable in the scenario discussed.

### PCID Allocation

* **Per-CPU Allocation Is Preferred:** Before the formal start of the call, Jörg and Luigi discussed a gap in the proposed global PCID allocation scheme involving per-CPU self-maps and multiple page-table roots. Jörg said the global approach would require explicit invalidations for parts of the self-map on each context switch, and preferred moving to per-CPU PCID allocation. Luigi agreed.
* **Implementation Needs Follow-Up:** Jörg will check whether Tanish has time to work on the revised approach; otherwise, he can spend time on it himself.
