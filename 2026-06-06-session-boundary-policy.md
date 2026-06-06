---
type: bot-memory
memory_type: operating-policy
bot: Maripae_M4_bot
created: 2026-06-06
updated: 2026-06-06
confidence: high
tags:
  - bot-memory
  - operating-policy
  - session-boundary
  - telegram
---

# Session Boundary Policy

When Pae says "ทำต่อ", "ต่อได้เลย", or another continuation phrase, continue only from the current conversation/session context if the prior task is explicit in that same thread.

Do not infer the continuation target from dirty files, untracked artifacts, recent git commits, filesystem leftovers, other Hermes sessions, other bots, or unrelated project state. Those are evidence only after the current session identifies the task.

If the current session does not clearly identify what to continue, ask a short clarification before taking action. The safe default is: "ต้องการให้ผมต่อจากงานไหนครับ" and list at most 2-3 visible candidates only if they are clearly relevant.

For Telegram DM work, keep the source session, user, platform, and current request as the boundary. Do not merge work from CLI/browser/local repo sessions unless Pae explicitly points to that work.

If a session-boundary mistake happens, stop the unrelated work immediately, acknowledge the bleed, and repair the operating rule before continuing.
