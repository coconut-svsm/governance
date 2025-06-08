# Meeting Minutes: SVSM Development Call (October 15th, 2025)

## Topics:

## Meeting Minutes

### Update from the TSC Meeting

* The TSC finished its discussion and is preparing a proposal for the handling of AI-generated code.
* The discussion on a policy for the **maintainership of repositories** under the COCONUT-SVSM GitHub organization is almost finished.
  * A document detailing the settled policy will be sent around next week for review and discussion at the next meeting.
* The TSC discussed several open Pull Requests (PRs), notably Richard's reboot PR.
* Discussion on the **SVSM specification ownership transition** is ongoing, with nothing fundamental to share at this time.

### Handling AI-Generated Code Proposal

* **Acceptance:** The TSC proposes to **accept AI-generated code**.
* **Human Responsibility (DCO):** The actual person submitting the code via a Pull Request (PR) is responsible for it, even if it is AI-generated.
  * The developer must ensure the code is correct, bug-free, and appropriately licensed.
* **AI Bots/Agents Submitting PRs:** Pull Requests opened by AI bots or agents **will not be accepted**, as this is seen as a violation of the Developer Certificate of Origin (DCO).
* **Exceptions for Bots:** Non-AI bots (like the GitHub DependaBot, which checks dependencies) will be decided on a case-by-case basis and are generally acceptable if they do not change code.
* **Legal and Licensing Context:**
  * The proposal is made in the best knowledge of the current situation, recognizing that policy may change with new legal information or gathered experience.
  * In US jurisdiction, code produced purely by an AI is a product of a machine and may not be copyrightable (public domain), making it compatible with any license.
  * Other jurisdictions, like Europe, may have a different stance.
  * Submitting developers must understand the **terms and conditions of the AI tool** used, as this affects licensing.
* **Next Step:** The proposal will be drafted into a document and sent out for further community review.

### Richard's Reboot PR Discussion

* **Action Item for Richard:** Richard is requested to write a **one-page document** describing the semantics of his current SVSM reset implementation.
  * This document should detail the expectations and assumptions a guest OS (like Linux at VMPL2) can make about the behavior of the reset command.
  * The document must specifically address the **TPM reset behavior** and reset behavior for other services provided by SVSM.

### Device Tree for SVSM

* **Status/Plan:** Luigi Leonardi reported he sent an email about the device tree and is working on the QEMU details but isn't ready to share yet.
* **Confirmation:** Jörg Rödel confirmed the plan is for the SVSM to consume a device tree file that only describes devices for the SVSM.
* **Implementation Details:** Luigi confirmed he modified `igvmbuilder`, and QEMU gets this and generates the device tree.
* **Assistance Offered:** Jörg offered to push his in-progress planes changes to a separate branch. This work includes changes to tag devices for different planes and can help Luigi figure out which devices are owned by SVSM.
* **Security Concern:** The group discussed the potential for Linux to access SVSM devices since MMIO and IO space is shared between all planes.

### TPM Reference Implementation Update

* **TPM PRs:** Stefano Garzarella opened a couple of Pull Requests (PRs) to update the Trusted Platform Module (TPM) code.
* **Reason for Update:** Jörg Rödel explained that the update was prompted because the upstream project removed Stefano's changes to make Pthreads optional.
* **Testing Request & Recommendation:** Stefano asked if someone could review and test the PRs.
* **Test Suite:** James Bottomley recommended using **Ken Goldman's `reg tests`** (part of the IBM TSS) as the next best option to the TCG's internal test suite.

### Container Script Removal

* **Status/Proposal:** Stefano noted that the container script is outdated, difficult to use (e.g., he couldn't find a way to specify the OVMF path), and questioned if it should be removed.
* **History:** Jörg Rödel explained the script was introduced historically because the SVSM project previously needed a specific environment due to build issues on distributions like Ubuntu or Fedora.
* **Current Status:** Jörg confirmed he is not using it and that SVSM "pretty much builds on all distributions" now (e.g., on Ubuntu).
* **Action:** Both agreed to "get rid of it".
