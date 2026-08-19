<!-- markdownlint-disable -->

# Hardening Report: jcs090218--setup-emacs/v2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **jcs090218--setup-emacs/v2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v2`, which is a mutable tag rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling supply-chain attacks. Replace with a full SHA pin, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/build.yml:22`
- `.github/workflows/test.yml:35`

### missing-permissions (severity: medium)

Neither workflow file defines a top-level `permissions:` block, and no job within either file defines its own `permissions:` block. Without explicit permissions, GitHub Actions defaults to the repository's default token permissions (often `write-all` for older repositories), granting the GITHUB_TOKEN broader access than necessary. Add a top-level `permissions: {}` (or minimal specific scopes) to both workflow files.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files (.github/workflows/build.yml and .github/workflows/test.yml):
1. unpinned-uses: Replaced `actions/checkout@v2` with the pinned SHA `actions/checkout@0717577d45739eb3c851188b29f50ed6c0b2194e # v2` in both files.
2. missing-permissions: Added top-level `permissions: {}` to both workflow files. For build.yml, the `dist` job also received `permissions: contents: write` at the job level since it performs `git push` to update the dist files — this follows least-privilege by keeping the top-level default locked down while granting only what the specific job needs.

