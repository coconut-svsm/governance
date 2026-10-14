# Meeting Minutes: SVSM Development Call (September 30th, 2026)

## Topics:

### TSC Meeting Update

* **New Release Completes the Host Branch Transition:** Jörg published a small release the previous day. The latest SVSM now requires the latest downstream Linux and QEMU host branches; it will not work with the older Linux 7.1 and QEMU 11.0 branches.
* **Release-Testing Documentation Extended:** Stefano's PR extending the release-testing documentation has been merged.
* **Deadlock Detection Needs More Design Work:** The TSC found problems with the proposed deadlock-detection approach. More investigation is needed before the design can work.
* **Attestation Testing in CI Is Being Explored:** Stefano is working on a PR to test parts of the attestation stack in CI. The environment limits coverage to the vsock path and communication with the KBS server, but these still cover a substantial part of the stack.
* **Root Build Script Removed:** Removal of the build script in the repository root has been merged. Its functionality can be replaced with an alias, and removing it frees the `build` name for a directory during repository reorganization.
* **VMR Design Remains Undecided:** The TSC again compared Jörg's PR 1215, which introduces a separate VMR type, with Carlos's approach, which unifies the implementations. Both have trade-offs, and no conclusion was reached. Jörg expects to make the final decision after further discussion in two weeks.

### Upstream Host Support

* **Planes Patches Await Updated Base Series:** Jörg is waiting for Paolo to post a new version of the architecture-independent base patches. He will then rebase the x86 and AMD-specific parts and post an updated upstream series.
* **Direct VMSA Is Now a Hard Requirement:** The recent VMSA placement change makes direct VMSA support mandatory for running SVSM. Jörg is waiting for Sean's feedback on the v2 series sent a few weeks earlier.
* **Restricted Injection Is Also Required:** The restricted-injection patch set must also be upstream before SVSM can run fully on upstream host components.

### Proposed TPM Command

* **Jeff Will Present in Two Weeks:** Jeff Andersen introduced a proposed TPM command, already sent to the mailing list, that would affect the vTPM in SVSM. The group agreed to defer the presentation to the next development call in two weeks so James can participate and provide feedback.
* **Detailed Review Is Still Pending:** Nicolai had seen the email and found the high-level idea interesting but had not yet reviewed the details.

### Rust TPM Implementation and Crypto Backends

* **TPM-RS Introduced:** Joe Richey from Google introduced the TCG-sponsored [TPM-RS project](https://github.com/tpm-rs/tpm-rs), which aims to reimplement the core logic of the C reference TPM in Rust. There is not yet an SVSM integration, but the team would like to present the approach and an example in two weeks. Jörg welcomed the effort and expressed interest in using a Rust TPM in SVSM.
* **Pluggable Crypto Is a Shared Goal:** TPM-RS is exploring pluggable crypto backends and post-quantum support. SVSM also needs backend flexibility, including OpenSSL and BoringSSL, and Nicolai and Oliver are working on a common crypto layer. The group saw no high-level conflict between these directions.
* **Shared Kernel/User-Space Crypto Remains a Longer-Term Goal:** SVSM aims to use a single crypto library that can be linked into both kernel and user mode. Jörg expects the project to handle this integration without imposing it on the TPM implementation.
* **Cocoon TPM Is Not Ready to Replace the Current TPM:** Nicolai explained that [Cocoon TPM](https://github.com/coconut-svsm/cocoon-tpm) began as a Rust TPM effort. Its CocoonFS storage backend and crypto components are complete, but the TPM logic is incomplete and remains in his local repository. Jörg suggested collaboration with TPM-RS.
* **TPM-RS Meeting Calendar Shared:** Joe also shared the project's [public meeting calendar](https://calendar.google.com/calendar/u/0/embed?src=c_1a544dd4bfc77581ce3a61227114b8ee9f71c88cee91fa17e51eedd9c98eb1e7@group.calendar.google.com&ctz=America/Los_Angeles).

### Early Boot Logging

* **Luigi Will Preserve Logs Before Console Initialization:** Messages logged before the console is initialized are currently lost. Luigi will work on buffering them and dumping them to the serial port once the console is available.
* **An Early Page Can Become the Log Buffer:** Jörg suggested reserving a page before memory management is active, logging to it, and later incorporating it into the normal log buffer. The approach will still not recover panic output if execution stops before console initialization.

### QEMU IGVM Command Line Support

* **Upstream Patch Posted:** Luigi posted a [QEMU patch for IGVM command line support](https://lore.kernel.org/qemu-devel/20260930-igvm_command_line-v1-1-62857007d89d@redhat.com/) and tested it with Jon's PR. It allows the command line to be set through QEMU, improving on the downstream patch that merely skips the IGVM directive.
* **Downstream Backport Will Follow Upstream Work:** Jörg invited Luigi to open a PR against the downstream QEMU repository. Luigi prefers to wait for upstream acceptance first to simplify later rebases.

### CocoonFS Format Change

* **Nicolai Is Considering a Small Format Change:** Nicolai asked whether anyone is already using CocoonFS, including for development testing. Adam said Google is not using it, and Jörg has not yet added it to his testing.
* **Usage Check Will Move to the Mailing List:** Nicolai will ask the wider community before proceeding. Jörg said recreating TPM state after a format change would be acceptable for his own testing, but other users should be consulted.

### Meeting Schedule

* **No Meetings Next Week:** There will be no TSC meeting or development call the following week because several contributors will attend Linux Plumbers Conference. The next development call is expected in two weeks, on October 14th, with the TPM command proposal and TPM-RS presentations planned.
