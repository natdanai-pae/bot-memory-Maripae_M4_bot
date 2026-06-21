---
type: bot-memory
memory_type: domain-reference
bot: Maripae_M4_bot
created: 2026-06-21
updated: 2026-06-21
confidence: high
tags:
  - bot-memory
  - bda
  - pm-log-api
  - daily-log
  - ai-usage
---

# BDA PM Log API

Reference from `BDA_PM_AI_LOG_API_USAGE_2026-06-21.md`.

## Endpoints

- JSON: `GET https://ai.bda.co.th/pm/logs.json`
- CSV: `GET https://ai.bda.co.th/pm/logs.csv`

## Authentication

Use a bearer token:

```http
Authorization: Bearer <PM_LOG_API_TOKEN>
```

Fallback header:

```http
X-BDA-PM-Log-Token: <PM_LOG_API_TOKEN>
```

Do not put the token in a query string, because it can leak through browser history, proxy logs, or tool logs.

Token file location on A40:

```text
/home/maripae/bda-ai-router/pm_log_api_token.txt
```

The file should be permission `600`. Share the token only through a private channel or password manager. Do not store the raw token value in memory notes.

## Query Parameters

- `days`: number of days back, for example `7`
- `from`: start date, for example `2026-06-19`
- `to`: end date, for example `2026-06-21`
- `q`: search important fields such as employee, project, task, outcome, and blocker
- `employee`: employee filter, for example `BDA103`
- `project`: project filter, for example `bangkok-spin`
- `status`: status filter, for example `closed`
- `limit`: max rows, up to `2000`

## Response Shape

Top-level JSON fields:

- `ok`
- `window`
- `query`
- `summary`
- `rows`

Summary includes sessions, closed/open/no_stop/blocked counts, usage requests, usage tokens, project count, and employee count.

Rows include employee code/name, project, tool, task, status, BKK start/latest timestamps, duration, steps, usage requests/tokens, models, outcome, next step, blocker, and session id.

The API does not export prompts, responses, API keys, raw token values, or credential/private key material.

## PM Lead AI Prompt

Use this instruction when PM Lead asks an AI to analyze team work with the API:

```text
คุณเป็น PM assistant ของ BDA
ให้เรียก BDA PM Log API เพื่อวิเคราะห์งานทีม
ห้ามเดาจาก token อย่างเดียว
ให้ดู session, project, task, outcome, next_step, blocker, duration, status และ usage_tokens ประกอบกัน
ถ้าข้อมูล metadata ไม่ครบ ให้ระบุว่า "ต้องถามพนักงานเพิ่ม"
ถ้ามี no stop/open session ให้จัดเป็น follow-up
ถ้ามี blocker ซ้ำ ให้เสนอ escalation
สรุปเป็น:
1. งานที่เสร็จแล้ว
2. งานที่ค้าง
3. blocker
4. คนที่ควร follow-up
5. project risk
6. คำถามที่ PM ควรถามทีม
```

