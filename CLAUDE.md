# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This repo holds GitHub Actions **workflows** (and, eventually, reusable **actions**) maintained by the
Checkmarx DevOps Scale and Security team, for use across other CheckmarxDev repos. There is no
application source code here — the deliverables are `.yml` workflow definitions under `.github/workflows/`.

## Repository structure

- `.github/workflows/` — workflow definitions, each independent and self-contained
- `.github/CODEOWNERS` — all files owned by `@checkmarxdev/cx-devops-scale-and-security`
- `README.md` — brief description of each workflow/action; keep it in sync when adding or renaming one

## Current workflows

- **github-actions-linter.yml** — runs on `pull_request`; lints the repo's own workflow/action YAML using
  Zizmor (`step-security/zizmor-action`), `persona: pedantic`, online audits disabled (no token available yet
  to read actions from other internal repos — see the `TODO` in the file).
- **trufflehog-secret-scan.yml** — runs on `pull_request` (main/master); scans PR commits for secrets using
  a pinned TruffleHog image (referenced by digest, tagged with version in a comment), posts/updates a single
  PR comment (marker-based upsert) summarizing findings, and fails the job only when a **verified** (live)
  secret is found. Unverified findings are warnings only and do not block merge.

## Conventions to follow when adding or editing workflows

- **Pin all third-party actions to a full commit SHA**, with the version as a trailing comment
  (e.g. `uses: actions/checkout@<sha> # v6.0.3`). Same pattern for Docker images: pin by digest with the
  human-readable tag/version in a trailing comment.
- **Default `permissions: {}` at the workflow level**; grant the minimum needed (`contents: read`, etc.) at
  the job level only.
- **Set `concurrency`** on PR-triggered workflows to avoid duplicate/overlapping runs — either a plain
  workflow/repo/ref group, or `cancel-in-progress: true` with a PR-number-scoped group when duplicate PR
  comments must be avoided.
- Non-obvious `bash` steps rely on `set -euo pipefail` (or `set -uo pipefail` when a non-zero grep match
  count is expected and handled explicitly) — preserve these when editing shell steps.
- Any new workflow or action added here should get a corresponding one- or two-line entry in `README.md`
  under the relevant "Actions" or "Workflows" section.
- Since this repo's own workflows are linted by `github-actions-linter.yml`, run that lint mentally (or via
  `zizmor` locally if available) against any new/changed workflow before considering the change done.
