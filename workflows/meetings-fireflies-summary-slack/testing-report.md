# testing-report.md — Meetings - Fireflies Summary - Slack

## Summary
| Test Type | Result |
|---|---|
| Happy path (success scenario) | ⚠️ Not run — submitted without test per submitter request |
| Induced error (failure handling) | ⚠️ Not run — submitted without test per submitter request |
| Notification path verification | ⚠️ Not run — submitted without test per submitter request |
| Edge cases | ⚠️ Not run — submitted without test per submitter request |

---

## Note on Testing
This workflow was submitted for review without a prior test execution. The reviewer should validate the following before approving:

1. **Fireflies credential** — confirm `Fireflies API Key` is configured in n8n as an HTTP Header Auth credential with `Authorization: Bearer <token>`
2. **Slack credential** — confirm `Slack OAuth2` is configured with `chat:write` and `channels:read` scopes
3. **#meetings channel** — confirm the channel exists and the Slack bot has been invited to it
4. **Fireflies GraphQL response shape** — confirm the `data.transcripts` path matches the live API response
5. **Date filtering** — confirm meeting `date` field from Fireflies is an ISO timestamp compatible with `new Date()`

---

## Expected Happy Path Behaviour
**Trigger:** Daily at 9:00am

**Expected node-by-node flow:**
| Node | Expected Output |
|---|---|
| Daily 9am Trigger | Fires, passes empty item downstream |
| Fetch Fireflies Meetings | Returns `{ data: { transcripts: [...] } }` from Fireflies GraphQL |
| Filter & Format Meetings | Filters to past-24h meetings; returns one formatted item per meeting |
| Post to #meetings | Posts one Slack message per meeting to #meetings |

**Expected Slack message format:**
```
*:movie_camera: [Meeting Title]*
:calendar: [Day, Month Date, Year]  :timer_clock: [X min]

*Summary*
[AI-generated overview from Fireflies]

*Action Items*
[Action items from Fireflies]
```

**No-meetings case:** If no meetings occurred in the past 24 hours, a single message is posted: `:calendar: No new meeting recordings found in the past 24 hours.`

---

## Test Environment
- **Mode:** Not tested
- **Tested by:** N/A — skipped at submitter request
- **Test date:** 2026-05-29
- **n8n Workflow ID:** K1bY275O7AyoJiAF
- **Registry ID:** 10eceeaf-ac40-44e7-86d2-77c926202b81
- **Instance:** fulcrumtest.app.n8n.cloud
