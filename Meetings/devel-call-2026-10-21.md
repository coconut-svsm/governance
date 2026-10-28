# Meeting Minutes: SVSM Development Call (October 21st, 2026)

## Topics:

### TSC Meeting Update

* **Stefano Hosted the Call:** Stefano Garzarella hosted in Jörg's absence.
* **Issue and PR Reviews Assigned:** The TSC reviewed open issues and PRs, checked their status, and assigned reviewers. Stefano reported no other major updates.

### Certify Integrated Follow-Up

* **Proposal Will Be Shared on the Mailing List:** Jeff Andersen followed up on the proposed `Certify Integrated` TPM command. James asked him to post a link to the presentation or a summary so people who were not on the previous call can follow the discussion through the mailing-list archive. Jeff agreed and said the presentation was intended to mirror the original proposal, with only the name changed. Stefano shared the [mailing-list discussion](https://lore.kernel.org/coconut-svsm/CADRsRuW1zJxk2+WxM2oQX1T_nq9O5SOoswhMQH+OsNvz9hUiHg@mail.gmail.com/) in chat.
* **Command Would Come Through the Reference Implementation:** James reiterated that Coconut would inherit the command from the TPM reference implementation after it is upstreamed to TCG. Jeff confirmed that this was also his understanding.
* **SVSM Would Need a Platform Hook:** Jeff noted that the current service-manifest attestation flow is separate from the service itself. James explained that integration would go through `libcrt`, wiring up the platform interface expected from the reference implementation. Jeff anticipated a new TPM-to-platform hook for SVSM to implement.
* **No Immediate Implementation Work Is Required:** Jeff set aside the earlier freshness discussion, describing the proposal as a standard mechanism for conveying the TPM's binding to the underlying root of trust. James expected adoption to be reasonably straightforward because it is equivalent to the existing functionality, if the project chooses to wire it up. The command is not yet available, and no immediate implementation work or final adoption decision was made.

### OpenSSL and LibCRT Refactoring

* **PR 1210 Separates Shared Dependencies from the vTPM:** Oliver Steffen explained [PR 1210](https://github.com/coconut-svsm/svsm/pull/1210), which moves OpenSSL out of the vTPM crate so SVSM can share one OpenSSL library across consumers. This also requires moving `libcrt` out of the vTPM crate into a top-level workspace crate, providing its C stub functions as a library for other crates to link against.
* **Rust-to-C Interface Cleanup Will Follow Separately:** Oliver has opened a follow-up issue and plans to clarify the interface between the Rust kernel and C libraries. Some functions are declared in `libcrt` but implemented and exported from scattered locations in the Rust code, making their origin unclear. Some exports are also gated by the vTPM feature and disappear when it is disabled, so they need to move to support other consumers. Oliver considers the work manageable and will bring ideas back for discussion in a few weeks.
* **PR Is Ready for Review:** Oliver fixed several issues, including ARM cross-building, and considers PR 1210 ready for review. Stefano will start reviewing it.
* **Patch Download Shared in Chat:** In response to James's request for a diffstat, Luigi shared the [PR patch series](https://patch-diff.githubusercontent.com/raw/coconut-svsm/svsm/pull/1210.patch), noting that it provides the individual patches and can be processed with `diffstat`. Luigi also pointed to GitHub's Files changed view for the overall diff, which shows the net changes across the series.
