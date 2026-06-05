---
type: bot-memory
memory_type: detailed-topic
bot: Maripae_M4_bot
created: 2026-05-16
updated: 2026-06-05
tags:
  - bot-memory
  - Maripae_M4_bot
  - jenkins
  - security
---

# Jenkins And Build Verification

## Build Expectations

User expects the assistant to verify Jenkins/build claims.

## Jenkins URL Memory

A Jenkins build URL/token was given in chat. Do not expose or copy secret tokens into public outputs or new notes. Treat it as sensitive operational credential.

## Rule

- Do not store build tokens in Obsidian memory notes.
- Do store the behavior: use the established Jenkins trigger path through the pipeline and verify build output.
- If user asks to trigger build, use the approved pipeline and confirm with logs/status.
- Do not prune/delete Jenkins jobs unless the user explicitly asks for the exact job names and confirms deletion.
- On 2026-06-05, a prune left only `innohub-ui`; jobs were restored from `/home/ubuntu/jenkins-job-prune-20260605-144913/jenkins-jobs-before-prune-20260605-144913.tgz`.
- Expected restored state is multiple BDA Jenkins jobs, not only InnoHub. Verified restored count: 61 jobs, including `innohub-ui`, `sxd-siamacc`, Siam Rent jobs, and `docker-cleanup`.
