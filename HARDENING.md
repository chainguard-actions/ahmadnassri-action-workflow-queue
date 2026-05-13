# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **ahmadnassri--action-workflow-queue/v1.1.2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml uses a Docker image reference with a mutable version tag instead of an immutable SHA digest. The image `docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.2` uses the tag `1.1.2`, which can be silently replaced with different (potentially malicious) content at any time. It should be pinned to a specific SHA digest, e.g. `docker://ghcr.io/ahmadnassri/action-workflow-queue@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:21`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image `ghcr.io/ahmadnassri/action-workflow-queue:1.1.2` to its immutable SHA256 digest `sha256:1f464bfdcc4ab819c89530fb753b7b1d96caf308be013fdbd77fa6532edeaf24`. The original tag `1.1.2` is preserved as a comment for readability.

