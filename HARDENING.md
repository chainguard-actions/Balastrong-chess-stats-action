<!-- markdownlint-disable -->

# Hardening Report: Balastrong--chess-stats-action/v1.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Balastrong--chess-stats-action/v1.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow uses 'actions/checkout@v3', which is pinned to a mutable tag ('v3') rather than a full 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling supply-chain attacks. Replace with a full SHA pin, e.g. 'actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v3'.

Locations:

- `.github/workflows/chess-test.yml:13`

### missing-permissions (severity: medium)

The workflow file '.github/workflows/chess-test.yml' has no top-level 'permissions:' key, and the only job ('update-readme') also has no job-level 'permissions:' key. Without explicit permissions, the GITHUB_TOKEN is granted its default (potentially broad) permissions. Add a top-level 'permissions:' block with the minimal scopes required (e.g. 'contents: write' if the action commits to the repo, and 'read-all' for everything else).

Locations:

- `.github/workflows/chess-test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both findings in .github/workflows/chess-test.yml: (1) Pinned actions/checkout@v3 to its full commit SHA f43a0e5ff2bd294095638e18286ca9a3d1956744, preserving the tag as a comment. (2) Added a top-level 'permissions: contents: write' block — the minimal scope required since the action writes updated chess stats back to the repository.

