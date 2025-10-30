# Meeting Minutes: SVSM Development Call (October 22nd, 2025)

## Topics:

### QEMU and Device Tree Work

* **Luigi Leonardi** reported on his progress working with **QEMU** over the past week.
  * He's successfully achieved **Device Tree** generation in QEMU for SVSM.
  * He **added the `plane` property** into the device tree.
  * **Jörg Rödel** confirmed this is valuable because the **SVSM** gets this property via the device tree, which allows the **guest VMPL to be configurable**.

### TSC Meeting Update

* **Jörg Rödel** provided a brief update from the previous TSC meeting.
* They reviewed policy documents but had no substantial changes requested.
* A couple of **PRs** were reviewed to ensure they were in a good state.
* One PR was merged: **Stefano's work to build the TPM using CMake**.
* **Action Item:** Users updating SVSM must now install **CMake** in their build environment to avoid breaking the build.
    * The build process still uses `cargo xbuild`.

### Upcoming Development Release

* The next development release is **due next week**.
* Any changes intended for this release must be **merged by then**.

### Daylight Saving Time Change

* **Europe** switches to wintertime next weekend (next Sunday).
* The **US** switches on November 2nd, a week later.
* Next week, the meeting time will **shift by one hour for everyone in America**.
* **Action Item:** US attendees should check the **community calendar on the Linux Foundation website** for the correct meeting time next week.

### Policy Discussions

#### AI Policy

* The AI policy document was discussed.
* One missing point was identified and will be added: a rule on **AI-based PR review and acceptance**.
  * **Rule:** AI tools are allowed to **assist in PR review**, but the **final merge decision must be made by a human**.
* The policy applies to **all repositories** under the COCONUT-SVSM project.
* The document serves as a **starting point** that can be changed over time as the community learns more about AI usage.

#### Repository Governance and Maintainership Policy

* A new policy on **repository governance and maintainership** within the Coconut SVSM GitHub project was presented.
* **Criteria for Hosting a Repository:** Repositories must be **relevant for the coconut ecosystem** and **actively maintained**.
* **Maintainership:**
  * Each repository needs **one or more maintainers**.
  * Maintainers have the power to make decisions on what gets merged and code review.
  * The **TSC** generally acts as an **observer** but may **intervene** in situations like security vulnerabilities, inactive maintainers, or co-maintainer disputes.
* **Best Practices & Responsibilities:**
  * Strongly encouraged to use a **pull request workflow** for all changes (for documentation and community review).
  * Maintainers must ensure all submissions follow the **Developer's Certificate of Origin (DCO)** (A script for this is available and can be part of CI).
  * Dependencies must be **actively maintained, up-to-date, and free from security vulnerabilities**.
  * Encouraged to use a **CODEOWNERS file** to document the maintainer structure.
  * Maintainers should be **responsive** in handling PRs and issues.
  * If not a downstream repository of another project (like QEMU or Linux), the repository must be licensed under the **MIT or APACHE-2.0 license**.
* This policy will be part of a future **PR to the governance repository**, and a mail will be posted to the mailing list for further comments.

### Planes Patch Set

* Jörg mentioned he sent a separate email to the mailing list about the **planes patch set** that was pushed to all repositories as separate branches.
* Attendees are **encouraged to test it** and provide feedback.
* The patch requires updating the **QEMU command line** to work.

### VGA None Issue (Issue 811)

* **Stefano Garzarella** brought up **Issue 811**, related to **QEMU** and the **VGA none** issue.
* **Vaishali Thakkar** confirmed she has not had time to look into it yet as she's focused on **SecureTSC** work.
* She will check if she can find time in the coming weeks.
