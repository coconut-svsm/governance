COCONUT-SVSM Repository Governance and Maintainership Policy
=============================================================

**Scope:** All repositories within the COCONUT-SVSM GitHub organization.

# Purpose and Philosophy

The goal of this policy is to ensure the health, continuity, and collaborative
spirit of all projects in the COCONUT-SVSM ecosystem. This document defines
roles and expectations for repository ownership and outlines the supportive
oversight role of the Technical Steering Committee ([TSC](../Groups/TSC.md)).

Our approach is designed to be supportive, empowering maintainers with autonomy
while ensuring project stability and compliance with the overall ecosystem
vision.

# Repository Hosting Criteria

For a new or existing repository to be hosted within the COCONUT-SVSM GitHub
organization, it must meet the following criteria:

* **Ecosystem Relevance:** The repository must be directly related to or
  functionally support the COCONUT-SVSM ecosystem. This includes, but is not
  limited to, core libraries, official tooling, documentation, and key
  integration components.
* **Active Maintainership:** Each repository must have at least one clearly
  designated maintainer or a team of maintainers responsible for its long-term
  viability and security.

# Governance and TSC Authority

## Technical Steering Committee (TSC) Access

To guarantee long-term project continuity and security, the
[TSC](../Groups/TSC.md) will be granted admin access to all repositories
within the organization.

* **Principle of Non-Intervention:** The [TSC](../Groups/TSC.md) will generally
  act as an observer.
  It will only intervene in a repository's operations if significant issues
  arise that threaten the project's continuity, security, or the stability of
  the wider COCONUT-SVSM ecosystem.
* **Intervention Triggers:** Intervention may occur in cases such as (but not
  limited to): security vulnerabilities, maintainer inactivity, or
  irreconcilable disputes among co-maintainers.

## Maintainer Ownership

Maintainers are the primary owners of their respective repositories and have
autonomy over daily operations, feature development, and code reviews, provided
they adhere to the best practices outlined in Section **Maintainer Roles and
Best Practices**.

# Maintainer Roles and Best Practices

Maintainers are responsible for the daily management, technical direction, and
quality control of their repository.

## The Pull Request (PR) Workflow

Maintainers are strongly encouraged to adopt a Pull Request (PR) based workflow
for all code changes, including changes made by single-maintainer projects.

Using PRs, even when merging one's own code, ensures that every change is
documented and had a chance to be reviewed by the community.

## Responsibilities

Maintainers must ensure:

* **Developer Certificate of Origin (DCO) Compliance:** All submissions to
  repositories must ensure compliance with the Developer Certificate of Origin
  (DCO).
* **Dependency Management:** Dependencies are kept up-to-date and free from
  known security vulnerabilities.
* **CODEOWNERS File:** Each repository is strongly encouraged to add a
  `CODEOWNERS` file documenting its maintainers structure.
* **Community Engagement:** Responsive handling of issues and
  community-submitted PRs (if applicable).
* **Licensing:** Repository which are not downstream forks of other open source
  projects must be licensed under the MIT or APACHE-2.0 license.

# Communication

This policy and its provisions are communicated with the goal of support and
clarity, not control. The measures related to TSC access are purely safeguards
for the long-term benefit of the ecosystem. We believe that clear guidelines
foster independence and stability. Any concerns regarding the application of
this policy should be directed to the TSC for review and discussion.
