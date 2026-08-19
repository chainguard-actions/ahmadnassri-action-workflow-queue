<!-- markdownlint-disable -->

# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **ahmadnassri--action-workflow-queue/v1.1.4** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml docker image reference uses a mutable version tag ('1.1.4') instead of a SHA digest, making it vulnerable to supply-chain attacks. Additionally, all uses: references in both workflow files use version tags instead of full 40-character SHA commit hashes. Unpinned references in pull_request_target.yml: actions/checkout@v3.5.2 (×2), ahmadnassri/action-metadata@v2.1.2, dependabot/fetch-metadata@v1.5.1, ahmadnassri/action-template-repository-sync@v2.3.4. Unpinned references in push.yml: actions/checkout@v3.5.2 (×4), ahmadnassri/action-metadata@v2.1.2, ahmadnassri/action-commit-lint@v2.1.9, oxsecurity/megalinter/flavors/javascript@v7.0.4, actions/upload-artifact@v3, ahmadnassri/action-semantic-release@v2.2.3, docker/setup-qemu-action@v2, docker/setup-buildx-action@v2, docker/login-action@v2, docker/build-push-action@v4, actions/github-script@v6, ahmadnassri/action-template-repository-sync@v2.3.4.

Locations:

- `action.yml:23`
- `.github/workflows/pull_request_target.yml:23`
- `.github/workflows/pull_request_target.yml:25`
- `.github/workflows/pull_request_target.yml:35`
- `.github/workflows/pull_request_target.yml:57`
- `.github/workflows/pull_request_target.yml:61`
- `.github/workflows/push.yml:22`
- `.github/workflows/push.yml:24`
- `.github/workflows/push.yml:33`
- `.github/workflows/push.yml:34`
- `.github/workflows/push.yml:40`
- `.github/workflows/push.yml:41`
- `.github/workflows/push.yml:45`
- `.github/workflows/push.yml:68`
- `.github/workflows/push.yml:72`
- `.github/workflows/push.yml:84`
- `.github/workflows/push.yml:85`
- `.github/workflows/push.yml:86`
- `.github/workflows/push.yml:89`
- `.github/workflows/push.yml:97`
- `.github/workflows/push.yml:131`
- `.github/workflows/push.yml:155`
- `.github/workflows/push.yml:156`

### broad-permissions (severity: medium)

push.yml sets top-level `permissions: read-all`, which grants overly broad read access to all scopes. This should be replaced with specific minimal permissions scoped to each job's actual needs.

Locations:

- `.github/workflows/push.yml:14`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions

**Notes:**

Fixed all unpinned action references by resolving them to full 40-character SHA commit hashes with tag comments for readability. Specifically: (1) action.yml: pinned docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.4 with its sha256 digest. (2) pull_request_target.yml: pinned actions/checkout@v3.5.2 (×2), ahmadnassri/action-metadata@v2.1.2, dependabot/fetch-metadata@v1.5.1, ahmadnassri/action-template-repository-sync@v2.3.4. (3) push.yml: pinned actions/checkout@v3.5.2 (×4), ahmadnassri/action-metadata@v2.1.2, ahmadnassri/action-commit-lint@v2.1.9, oxsecurity/megalinter/flavors/javascript@v7.0.4, actions/upload-artifact@v3, ahmadnassri/action-semantic-release@v2.2.3, docker/setup-qemu-action@v2, docker/setup-buildx-action@v2, docker/login-action@v2, docker/build-push-action@v4, actions/github-script@v6, ahmadnassri/action-template-repository-sync@v2.3.4. Also replaced the broad `permissions: read-all` in push.yml with `permissions: contents: read` — the minimal permission needed for read-only jobs, while write-access jobs already have their own job-level permissions blocks.

