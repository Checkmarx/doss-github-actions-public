# DOSS GitHub Actions

GitHub actions and workflows maintained by the CX [cx-sec-pub team](https://github.com/orgs/Checkmarx/teams/cx-sec-pub).

## Actions

TBD

## Workflows

***github-actions-linter***

This workflow runs style and security checks against a repo's GitHub workflow and action definitions.

***trufflehog-secret-scan***

This workflow scans a pull request's commits for secrets using TruffleHog, posting/updating a single PR comment with the findings and blocking the merge if a verified (live) secret is found.
