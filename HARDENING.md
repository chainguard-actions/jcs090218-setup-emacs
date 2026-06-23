<!-- markdownlint-disable -->

# Hardening Report: jcs090218--setup-emacs/v3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **jcs090218--setup-emacs/v3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both composite action steps in action.yml reference external actions using the mutable branch ref `@master` instead of a pinned 40-character commit SHA. If either upstream repository (`purcell/setup-emacs` or `jcs090218/setup-emacs-windows`) is compromised or force-pushed, the action will silently execute attacker-controlled code. Failing references: `purcell/setup-emacs@master` (line 12) and `jcs090218/setup-emacs-windows@master` (line 15). Each should be pinned to a full SHA, e.g. `purcell/setup-emacs@<40-char-sha> # master`.

Locations:

- `action.yml:12`
- `action.yml:15`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned both mutable @master references in action.yml to full commit SHAs: `purcell/setup-emacs@master` → `purcell/setup-emacs@509bfe03ba1ffddb67b3c6d9eaaeb96b45182cc7 # master` (line 12) and `jcs090218/setup-emacs-windows@master` → `jcs090218/setup-emacs-windows@64cc4c9b396a66b838820fd465be52b08cc279cc # master` (line 15). SHAs were resolved using the GitHub API via lookup_action_sha.

