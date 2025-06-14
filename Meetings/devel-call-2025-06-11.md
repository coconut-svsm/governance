# Meeting Minutes: SVSM Development Call (June 11th, 2025)

## Topics:

### Confidential Computing Consortium (CCC) Annual Project Update

* Jörg Rödel will present the COCONUT-SVSM project update at the CCC Technical Advisory Council meeting.
* The presentation will cover:
  * Project progress during the past year.
  * Milestones achieved since joining the consortium.
  * A preview of the slide deck was shared for review and feedback.
* Attendees were invited to suggest improvements or corrections to the slides.

### Consolidation of Cryptographic Libraries

* Background:
  * Multiple cryptographic implementations are currently used within the SVSM codebase.
  * A new implementation is being introduced with the KBS attestation pull request (PR), potentially making it the third crypto library.
  * This raised concerns during a Technical Steering Committee meeting and prompted a discussion on consolidation.
* Discussion Points:
  * Jörg Rödel initiated the topic, noting the goal of reducing duplication and avoiding further fragmentation.
  * Nicolai Stange provided an overview of the cocoon-tpm crypto crate, which he has been developing:
    * Initially built as an abstraction over the RustCrypto libraries for symmetric algorithms.
    * Includes custom implementations for some asymmetric algorithms.
    * Supports BoringSSL as an alternative backend and could potentially add OpenSSL support in the future.
    * The library is seen as a good candidate for unifying crypto functionality across the project.
* Follow-ups:
  * Jörg asked whether existing uses of RustCrypto in the SVSM could be replaced by Nicolai's library.
  * Nicolai confirmed this would be feasible and suggested future extensions to support additional cryptographic backends.
  *  Although the current KBS attestation PR introduces another library, the team agreed it wouldn’t be blocked, as it may serve as a starting point for consolidation.

### Logging Infrastructure and Debugging Use Cases

* Context:
  * The topic was raised following discussions in the Technical Steering Committee (TSC) meeting related to pending pull requests.
  * A key question: Should the hypervisor have visibility into SVSM logs for debugging purposes?
* Discussion Points:
  * The current log buffer mechanism may be changed to log everything to a file object, effectively persisting logs within the SVSM.
  * There is a need to define use cases for logs:
    * Crash diagnostics: Exporting logs to the hypervisor may help debug crashes.
    * Service-level separation: Debate whether logs should be stored per service or aggregated.
    * Security and privacy: Concerns about exposing logs to the hypervisor by default.
* Ideas Proposed:
  * Make logging configurable by the guest: Guests could enable a "debug mode" to expose logs in case of failures.
  * When persistent storage becomes available: Store logs there to preserve them across crashes.
  * Provide a tool to decrypt and extract logs from storage by the guest owner.
  * Consider direct I/O and integrity protection for stored log files to ensure reliability and trustworthiness.
* Open Questions:
  * What should the default behavior be?
  * How can logs be accessed if SVSM itself crashes?
  * Should crash logging be opt-in per deployment, especially for sensitive workloads?

### EFI Variables Protocol and Secure Boot

* Context: The EFI Variables (UEFI) service was acknowledged as a critical missing piece for enabling Secure Boot functionality in SVSM, particularly on AMD platforms.
* Gerd is working on implementing the EFI Variable Store and has a prototype running.
* His setup can already boot a Linux guest with Secure Boot enabled.
* Current status of the prototype:
  * Microsoft Secure Boot certificates are hardcoded.
  * The variable store is not yet persistent, as SVSM still lacks persistent storage support.
  * Each reboot results in a fresh, empty EFI variable store.
  * Signature verification support is missing, which prevents secure runtime updates of the secure boot variables.
* Technical Strategy:
  * Gerd proposed splitting the implementation into two pull requests:
  * One to reserve the protocol number, enabling forward compatibility.
  * Another to implement the actual protocol without causing merge conflicts with other protocol additions.
* Conclusion:
  * Even a basic implementation without persistence or signature updates may be sufficient for initial use cases.
  * Jörg Rödel acknowledged this as valuable progress and agreed with the staged integration strategy.
