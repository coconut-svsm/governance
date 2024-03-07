# Meeting: SVSM Development Call (February 14, 2024)

## Attendees:

Adam Dunlap, Carlos, Carlos Bilbao, Carlos López, David Altobelli, Eddie Dong, Jacob Xu, Jeremi Piotrowski, Joerg Roedel, Liam Merwick, Nicolai Stange, Oliver Steffen, Roy Hopkins, Vasant Karasulli, Vijay dhanraj

## Announcements:

* Joerg Roedel will be out next week, so there will be no SVSM development call on February 21st.

## Topics:

### Move to IGVM as the default launch process for SVSM:

* Joerg Roedel proposed switching the default launch process for SVSM to IGVM.
* Roy Hopkins reported a build issue with IGVM and suggested creating an issue on the IGVM repo.
* Joerg Roedel suggested waiting until Friday to merge the necessary changes to allow everyone to try out the new process and report any issues.
* After Friday, if no issues are reported, the changes will be merged and support for the old launch process (stage1) will eventually be removed.
* Documentation on how to use the new process is available in Roy Hopkins' PR #237.
* Oliver Steffen asked about the possibility of having a tool to calculate SNP measurements with IGVM. Joerg Roedel suggested requesting an attestation report to get the launch measurement.

### Continuous Integration (CI) on actual SMP-capable hardware:

* Jeremi Piotrowski inquired about the status of CI on SMP-capable hardware.
* Joerg Roedel mentioned limited availability of hardware and the need for additional resources from the CCC project.
* He expressed interest in getting the project onboarded with the CCC to enable CI.

### IGVM file signing and ID blocks:

* David Altobelli offered to contribute to the IGVM tooling related to signing and ID blocks.
* Joerg Roedel mentioned that signing is not yet implemented but planned for the future.

### Code ownership and review process:

* Joerg Roedel mentioned using labels for PRs to track their status.
* Carlos López suggested using GitHub's code owners feature to automate review requests.
* Joerg Roedel expressed interest in implementing this feature.

### Replacement of remaining Box uses with the new type:

* Carlos López announced the completion of the new Box type and its almost complete equivalence to the old one.
* He mentioned a small detail about unsized types requiring a macro due to technical limitations.

### Deprecation of stage1 launch process:

* Jacob Xu inquired about the timeline for deprecating the stage1 launch process.
* Joerg Roedel suggested a staged approach:
  * Merge the IGVM documentation changes first, allowing users to continue using the old process.
  * Encourage everyone to switch to IGVM.
  * After sufficient adoption, remove the stage1 code and dependencies.
* Adam Dunlap requested keeping stage1 available longer as Google cannot easily switch due to using a different VMM. Joerg Roedel agreed, as long as Google reports any issues encountered.

