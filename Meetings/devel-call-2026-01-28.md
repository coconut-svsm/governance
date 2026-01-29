# Meeting Minutes: SVSM Development Call (January 28th, 2026)

## Topics:

### **TSC Meeting Updates**

* **Google Summer of Code (GSoC)**: Mentors have been identified for the two pending items.
  * An appeal was made for additional volunteer mentors to help manage workloads during summer vacations. Interested parties should reply to Stefano’s email thread.
* **Upcoming Release**: * A new release is scheduled for tomorrow (January 29th) morning European time.
  * Merging of new Pull Requests (PRs) is paused until the release is finalized.
  * Verification testing was recently broken and requires follow-up with the Microsoft Research team.
* **TPM Licensing/TCG Language**:
  * There is an ongoing process to remove a specific warning from the Trusted Computing Group (TCG) header.
  * The change requires sign-off from all member company councils, making the timeline open-ended.
  * James Bottomley noted that the current "OIN patent shield" provides stronger protection than the BSD license regardless of the warning.

### **COCOON-FS Technical Discussion**

* **Encryption Modes**:
  * The group discussed the trade-offs between the current AES-CBC mode (high security but requires full file rewrites) and other modes like XTS that allow random access/in-place updates.
  * While current use cases (TPM/UEFI state) involve small files, the group agreed to reserve a "bit flag" in the data structures to allow future extensibility for other encryption modes without breaking compatibility.
* **Comparison to existing headers**:
  * James Bottomley suggested considering headers from **dm-crypt** or **FSVerity** to handle algorithm selection.
  * Nicolai Stange clarified that CocoonFS's unique requirement is full filesystem authentication, which dm-crypt does not provide out-of-the-box.
* **New Feature Requests**:
  * **Metadata Profiles**: A request to allow separate metadata profiles per inode, which could be used by SVSM for permission information.
  * **Plain Text Global Header**: A proposal for a clear-text field in the filesystem header. This would store a "wrapped key" for the Key Broker Service (KBS) to facilitate attestation before full decryption.
  * **Header Format**: The proposed format for this header includes a 16-byte global UID followed by a data blob defined by that UID.
