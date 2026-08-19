<!-- markdownlint-disable -->

# Hardening Report: rematocorp--trello-integration-action/v9.11.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **rematocorp--trello-integration-action/v9.11.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### permissions (severity: medium)

The workflow file .github/workflows/ci.yml has no top-level `permissions:` key and the only job (`test`) also has no job-level `permissions:` key. This means the workflow runs with the default (broad) GitHub token permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci.yml:1`

### unpinned-uses (severity: high)

The workflow .github/workflows/ci.yml references three actions by mutable version tags instead of immutable 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved: `actions/checkout@v4` (line 15), `actions/setup-node@v4` (line 18), `codecov/codecov-action@v4.0.1` (line 32). Each should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ci.yml:15`
- `.github/workflows/ci.yml:18`
- `.github/workflows/ci.yml:32`

## Iteration Notes

### Iteration 1

**Fixes applied:** permissions, unpinned-uses

**Notes:**

Fixed .github/workflows/ci.yml: (1) Added top-level `permissions: contents: read` to enforce least-privilege GitHub token access. (2) Pinned all three action references to immutable full commit SHAs: actions/checkout@v4 → 11d5960a326750d5838078e36cf38b85af677262, actions/setup-node@v4 → 49933ea5288caeca8642d1e84afbd3f7d6820020, codecov/codecov-action@v4.0.1 → e0b68c6749509c5f83f984dd99a76a1c1a231044. Original version tags preserved as inline comments.

