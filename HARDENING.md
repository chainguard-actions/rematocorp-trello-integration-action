<!-- markdownlint-disable -->

# Hardening Report: rematocorp--trello-integration-action/v9.11.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rematocorp--trello-integration-action/v9.11.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The workflow file .github/workflows/ci.yml references three GitHub Actions using mutable tags instead of pinned full-length SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code. Failing references: (1) actions/checkout@v4, (2) actions/setup-node@v4, (3) codecov/codecov-action@v4.0.1. Each should be replaced with the corresponding 40-character hex commit SHA (e.g. actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4).

Locations:

- `.github/workflows/ci.yml:14`
- `.github/workflows/ci.yml:17`
- `.github/workflows/ci.yml:27`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and the single job `test` also has no `permissions:` key. Without explicit permissions, the workflow inherits the default repository permissions (which may include write access to contents, pull-requests, etc.), violating the principle of least privilege. A `permissions:` block with only the minimal required scopes (e.g. `contents: read`) should be added at the top level or on the job.

Locations:

- `.github/workflows/ci.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed .github/workflows/ci.yml: (1) Pinned actions/checkout@v4 to SHA 34e114876b0b11c390a56381ad16ebd13914f8d5, actions/setup-node@v4 to SHA 49933ea5288caeca8642d1e84afbd3f7d6820020, and codecov/codecov-action@v4.0.1 to SHA e0b68c6749509c5f83f984dd99a76a1c1a231044, preserving original tags in comments. (2) Added top-level `permissions: contents: read` block to enforce least-privilege access.

