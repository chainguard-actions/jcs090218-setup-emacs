<!-- markdownlint-disable -->

# Hardening Report: jcs090218--setup-emacs/v1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **jcs090218--setup-emacs/v1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference `actions/checkout@v2`, which is a mutable tag rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling supply-chain attacks. Each reference should be replaced with the full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v2`.

Locations:

- `.github/workflows/build.yml:22`
- `.github/workflows/test.yml:34`

### missing-permissions (severity: medium)

Neither workflow file declares a top-level `permissions:` block, and neither job within them declares job-level permissions. Without explicit permissions, GitHub grants the default (often `write` for `GITHUB_TOKEN`), which violates the principle of least privilege. A minimal `permissions:` block (e.g. `contents: read`) should be added at the top level or per-job.

Locations:

- `.github/workflows/build.yml:1`
- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed both workflow files: (1) Pinned `actions/checkout@v2` to its full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` in both build.yml and test.yml, preserving the tag as a comment. (2) Added top-level `permissions:` blocks — `contents: write` in build.yml (required because the workflow commits and pushes dist files) and `contents: read` in test.yml (minimal read-only access sufficient for checkout and testing).

