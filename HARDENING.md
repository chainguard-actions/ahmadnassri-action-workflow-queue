<!-- markdownlint-disable -->

# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ahmadnassri--action-workflow-queue/v1.1.3** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in workflow files are pinned to mutable version tags instead of immutable 40-character SHA commit hashes, making them vulnerable to supply-chain attacks. Unpinned references in pull_request_target.yml: `actions/checkout@v3.5.2`, `ahmadnassri/action-metadata@v2.1.2`, `dependabot/fetch-metadata@v1.5.1`, `ahmadnassri/action-template-repository-sync@v2.3.4`. Unpinned references in push.yml: `actions/checkout@v3.5.2` (multiple), `ahmadnassri/action-metadata@v2.1.2`, `ahmadnassri/action-commit-lint@v2.1.9`, `oxsecurity/megalinter/flavors/javascript@v7.0.4`, `actions/upload-artifact@v3`, `ahmadnassri/action-semantic-release@v2.2.3`, `docker/setup-qemu-action@v2`, `docker/setup-buildx-action@v2`, `docker/login-action@v2`, `docker/build-push-action@v4`, `actions/github-script@v6`, `ahmadnassri/action-template-repository-sync@v2.3.4`. Additionally, action.yml references a mutable Docker image tag `docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.3` instead of a SHA digest.

Locations:

- `.github/workflows/pull_request_target.yml:21`
- `.github/workflows/pull_request_target.yml:23`
- `.github/workflows/pull_request_target.yml:34`
- `.github/workflows/pull_request_target.yml:57`
- `.github/workflows/pull_request_target.yml:66`
- `.github/workflows/push.yml:26`
- `.github/workflows/push.yml:29`
- `.github/workflows/push.yml:40`
- `.github/workflows/push.yml:48`
- `.github/workflows/push.yml:55`
- `.github/workflows/push.yml:57`
- `.github/workflows/push.yml:68`
- `.github/workflows/push.yml:87`
- `.github/workflows/push.yml:96`
- `.github/workflows/push.yml:103`
- `.github/workflows/push.yml:104`
- `.github/workflows/push.yml:105`
- `.github/workflows/push.yml:107`
- `.github/workflows/push.yml:121`
- `.github/workflows/push.yml:148`
- `.github/workflows/push.yml:163`
- `.github/workflows/push.yml:172`
- `action.yml:20`

### broad-permissions (severity: medium)

The workflow file push.yml sets `permissions: read-all` at the top level. This grants overly broad read access across all permission scopes and should be replaced with specific minimal permissions required by each job.

Locations:

- `.github/workflows/push.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions

**Notes:**

Fixed all unpinned `uses:` references in pull_request_target.yml and push.yml by resolving each tag to its full 40-character SHA commit hash (preserving the tag as a comment). Pinned the Docker image in action.yml to its immutable SHA digest while preserving the `docker://` scheme and tag. Replaced the broad `permissions: read-all` in push.yml with `permissions: {}` at the top level and added specific minimal permissions to each job that requires them.

