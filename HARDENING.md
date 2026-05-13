# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.4

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **ahmadnassri--action-workflow-queue/v1.1.4** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image referenced by a mutable version tag instead of an immutable SHA digest. `image: docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.4` uses the tag `1.1.4`, which can be silently overwritten to point to a different (potentially malicious) image. It should be pinned to a specific SHA digest, e.g. `image: ghcr.io/ahmadnassri/action-workflow-queue@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:23`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.4` with the immutable SHA256 digest `docker://ghcr.io/ahmadnassri/action-workflow-queue@sha256:35e3262089d67eeddfd965a6d921b73b6526a53b045ce22243a404fe56251eed # 1.1.4` in action.yml line 23.

