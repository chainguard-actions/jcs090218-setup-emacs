<!-- markdownlint-disable -->

# Hardening Report: jcs090218--setup-emacs/v3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **jcs090218--setup-emacs/v3** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml references two external actions using mutable branch refs (@master) instead of pinned 40-character commit SHAs. If the upstream repositories are compromised or the branch is force-pushed, the action will silently execute attacker-controlled code. Failing references: 'purcell/setup-emacs@master' and 'jcs090218/setup-emacs-windows@master'.

Locations:

- `action.yml:9`
- `action.yml:12`

### unpinned-uses (severity: high)

.github/workflows/test.yml references 'actions/checkout@v6' using a mutable version tag instead of a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time.

Locations:

- `.github/workflows/test.yml:49`

### missing-permissions (severity: medium)

.github/workflows/test.yml has no top-level 'permissions:' key and the single job ('build') also has no 'permissions:' key. Without explicit permissions, the workflow inherits the default token permissions (which may be read/write depending on repository settings), granting broader access than necessary.

Locations:

- `.github/workflows/test.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all three findings: (1) Pinned purcell/setup-emacs@master to SHA 1f1e9c315c2e3312705e920ae1ddd7e0e2b13c69 in action.yml; (2) Pinned jcs090218/setup-emacs-windows@master to SHA ae405f3dc2c8699b25bda8824850cfec5ec98b1b in action.yml; (3) Pinned actions/checkout@v6 to SHA df4cb1c069e1874edd31b4311f1884172cec0e10 in .github/workflows/test.yml; (4) Added top-level 'permissions: {}' to .github/workflows/test.yml to enforce least-privilege token access. All mutable branch/tag refs replaced with immutable 40-character commit SHAs while preserving the original ref in a trailing comment for readability.

