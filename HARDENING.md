# Hardening Report: ahmadnassri--action-workflow-queue/v1.1.3

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **ahmadnassri--action-workflow-queue/v1.1.3** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yml runs.image field references a Docker image using a mutable version tag (1.1.3) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the tag, creating a supply-chain attack risk. The failing reference is: `image: docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.3`. It should be pinned to a SHA digest, e.g. `image: ghcr.io/ahmadnassri/action-workflow-queue@sha256:<64-hex-char-digest>`.

Locations:

- `action.yml:22`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://ghcr.io/ahmadnassri/action-workflow-queue:1.1.3` with the immutable SHA digest `docker://ghcr.io/ahmadnassri/action-workflow-queue@sha256:b428880788d110da6ec3043486b40f822aad120b036cc7d7dd20a5975cad5a14 # 1.1.3` in action.yml line 22. The original tag is preserved as a comment for readability.

