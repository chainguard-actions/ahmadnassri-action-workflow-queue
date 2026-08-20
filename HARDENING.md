<!-- markdownlint-disable -->

# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ahmadnassri--action-workflow-queue/v1.1.2** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml docker image reference uses a mutable version tag instead of a SHA digest: `image: docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.2`. Additionally, all `uses:` references in both workflow files use version tags (e.g. @v3.5.2, @v2.1.2, @v1.5.1, @v7.0.4, @v2, @v4, @v6) rather than pinned 40-character commit SHAs. Unpinned references are vulnerable to supply-chain attacks if the upstream tag is moved or the image is replaced. Affected references include: actions/checkout@v3.5.2, ahmadnassri/action-metadata@v2.1.2, dependabot/fetch-metadata@v1.5.1, ahmadnassri/action-template-repository-sync@v2.3.4, ahmadnassri/action-commit-lint@v2.1.9, oxsecurity/megalinter/flavors/javascript@v7.0.4, actions/upload-artifact@v3, ahmadnassri/action-semantic-release@v2.2.3, docker/setup-qemu-action@v2, docker/setup-buildx-action@v2, docker/login-action@v2, docker/build-push-action@v4, actions/github-script@v6.

Locations:

- `action.yml:20`
- `.github/workflows/pull_request_target.yml:21`
- `.github/workflows/pull_request_target.yml:23`
- `.github/workflows/pull_request_target.yml:33`
- `.github/workflows/pull_request_target.yml:57`
- `.github/workflows/pull_request_target.yml:60`
- `.github/workflows/push.yml:24`
- `.github/workflows/push.yml:29`
- `.github/workflows/push.yml:38`
- `.github/workflows/push.yml:44`
- `.github/workflows/push.yml:51`
- `.github/workflows/push.yml:56`
- `.github/workflows/push.yml:72`
- `.github/workflows/push.yml:97`
- `.github/workflows/push.yml:100`
- `.github/workflows/push.yml:101`
- `.github/workflows/push.yml:103`
- `.github/workflows/push.yml:109`
- `.github/workflows/push.yml:130`
- `.github/workflows/push.yml:155`
- `.github/workflows/push.yml:163`

### broad-permissions (severity: medium)

The push.yml workflow sets top-level `permissions: read-all`, which grants overly broad read access across all scopes. This should be replaced with specific minimal permissions scoped to only what each job requires.

Locations:

- `.github/workflows/push.yml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions

**Notes:**

Fixed all unpinned action references by resolving each tag to its full 40-character commit SHA: actions/checkout@v3.5.2→8e5e7e5, ahmadnassri/action-metadata@v2.1.2→c292173, dependabot/fetch-metadata@v1.5.1→cd6e996, ahmadnassri/action-template-repository-sync@v2.3.4→a6390c0, ahmadnassri/action-commit-lint@v2.1.9→33a0f3d, oxsecurity/megalinter/flavors/javascript@v7.0.4→0d014ff, actions/upload-artifact@v3→ff15f03, ahmadnassri/action-semantic-release@v2.2.3→b9ed9c1, docker/setup-qemu-action@v2→2b82ce8, docker/setup-buildx-action@v2→885d146, docker/login-action@v2→465a078, docker/build-push-action@v4→0a97817, actions/github-script@v6→d7906e4. The docker image in action.yml was pinned with its sha256 digest (1f464bf) while preserving the docker:// scheme and tag. The broad `permissions: read-all` in push.yml was replaced with `permissions: contents: read` (minimal needed at top level), with job-level permissions blocks already in place for jobs requiring elevated access.

