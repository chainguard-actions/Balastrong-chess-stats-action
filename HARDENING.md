<!-- markdownlint-disable -->

# Hardening Report: Balastrong--chess-stats-action/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Balastrong--chess-stats-action/v2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference GitHub Actions using mutable tags instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks if the referenced tag is moved or the upstream repository is compromised.

Failing references:
- `.github/workflows/chess-test.yml` line 16: `uses: actions/checkout@v3`
- `.github/workflows/code-check.yml` line 17: `uses: actions/checkout@v2`
- `.github/workflows/code-check.yml` line 18: `uses: actions/setup-node@v1`

Each should be replaced with the full 40-character commit SHA, e.g. `uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3`.

Locations:

- `.github/workflows/chess-test.yml:16`
- `.github/workflows/code-check.yml:17`
- `.github/workflows/code-check.yml:18`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` key, and no job-level `permissions:` key is present in any job. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (which may be `write-all` for older repositories), granting unnecessarily broad access. A minimal `permissions:` block (e.g. `contents: write` for the chess-test workflow that commits to the repo, and `contents: read` for the code-check workflow) should be added.

Locations:

- `.github/workflows/chess-test.yml:1`
- `.github/workflows/code-check.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three unpinned action references by resolving their full commit SHAs via lookup_action_sha and updating the uses: lines with the format 'owner/repo@<sha> # tag'. Added top-level permissions blocks to both workflow files: 'contents: write' for chess-test.yml (which commits updated stats back to the repo) and 'contents: read' for code-check.yml (which only reads the repo for CI checks).

