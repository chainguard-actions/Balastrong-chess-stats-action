<!-- markdownlint-disable -->

# Hardening Report: Balastrong--chess-stats-action/v2.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Balastrong--chess-stats-action/v2.0.1** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Workflow uses mutable tag references instead of pinned full-length SHA commit hashes, making the workflow vulnerable to supply-chain attacks if the referenced tag is moved or overwritten. Failing references: `actions/checkout@v3` (line 16).

Locations:

- `.github/workflows/chess-test.yml:16`

### unpinned-uses (severity: high)

Workflow uses mutable tag references instead of pinned full-length SHA commit hashes, making the workflow vulnerable to supply-chain attacks if the referenced tags are moved or overwritten. Failing references: `actions/checkout@v2` (line 18), `actions/setup-node@v1` (line 19).

Locations:

- `.github/workflows/code-check.yml:18`
- `.github/workflows/code-check.yml:19`

### missing-permissions (severity: medium)

Workflow has no top-level `permissions:` key and the single job (`update-readme`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Add a `permissions:` block with the minimum required scopes (e.g., `contents: write` if committing to the repo).

Locations:

- `.github/workflows/chess-test.yml:1`

### missing-permissions (severity: medium)

Workflow has no top-level `permissions:` key and the single job (`test`) also has no `permissions:` key. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad. Add a `permissions:` block with the minimum required scopes (e.g., `contents: read`).

Locations:

- `.github/workflows/code-check.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four findings across two workflow files:

1. `.github/workflows/chess-test.yml`:
   - Pinned `actions/checkout@v3` → `actions/checkout@a37ce9120846195fa4ece8f58b268e6043cb2f26 # v3`
   - Added top-level `permissions: contents: write` (the workflow commits updated README files)

2. `.github/workflows/code-check.yml`:
   - Pinned `actions/checkout@v2` → `actions/checkout@0717577d45739eb3c851188b29f50ed6c0b2194e # v2`
   - Pinned `actions/setup-node@v1` → `actions/setup-node@f1f314fca9dfce2769ece7d933488f076716723e # v1`
   - Added top-level `permissions: contents: read` (minimum needed for checkout and running CI tests)

