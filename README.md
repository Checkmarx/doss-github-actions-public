# DOSS GitHub Actions

GitHub actions and workflows maintained by the CX [cx-sec-pub team](https://github.com/orgs/Checkmarx/teams/cx-sec-pub).

## Actions

TBD

## Workflows

***github-actions-linter***

This workflow runs style and security checks against a repo's GitHub workflow and action definitions.

***trufflehog-secret-scan***

This workflow scans a pull request's commits for secrets using TruffleHog, posting/updating a single PR comment with the findings and blocking the merge if a verified (live) secret is found.

****-test***

Internal harnesses that call the corresponding workflow above via `workflow_call` using the PR-branch's own version, so edits to that workflow are exercised in the PR rather than only the org ruleset's pinned copy. Triggered when a PR touches the real workflow file or the harness itself.
