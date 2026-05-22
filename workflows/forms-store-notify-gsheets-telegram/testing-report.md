# testing-report.md — Forms - Store and Notify - Google Sheets and Telegram

## Summary
| Test Type | Result |
|---|---|
| Happy path (success scenario) | ✅ Pass |
| Credential-dependent nodes (pinned) | ✅ Pass |
| Field extraction logic | ✅ Pass |
| Execution log output | ✅ Pass |

---

## Happy Path Test

**Mode:** Safe Test (pin data — no real external calls)

**Input used:**
```json
{
  "body": {
    "name": "Ravi Sharma",
    "email": "ravi.sharma@fulcrumapp.com",
    "message": "Testing the Google Form integration workflow",
    "timestamp": "2026-05-22T10:30:00Z"
  }
}
```

**Node-by-node results:**
| Node | Status | Output Summary |
|---|---|---|
| Google Form Submission | ✅ Pinned | Simulated POST body with name, email, message, timestamp |
| Extract Form Fields | ✅ Success | Extracted: name=Ravi Sharma, email=ravi.sharma@fulcrumapp.com, message=Testing..., submittedAt=2026-05-22T10:30:00Z |
| Store in Google Sheets | ✅ Pinned | Simulated successful row append (credentials not configured yet) |
| Send Telegram Notification | ✅ Pinned | Simulated message sent (ok: true, message_id: 4201) |
| Log Execution Status | ✅ Success | status=SUCCESS, executedAt=2026-05-22T09:32:15.708-04:00, submitter=Ravi Sharma, sheetsRowAppended=true, telegramNotified=true |

**Overall outcome:** All 5 nodes executed in sequence. Execution completed in 43ms. Field extraction resolved correctly from nested `body` object. Log node accurately reflected the submission context.

---

## Credential-Dependent Node Pinning

The **Store in Google Sheets** and **Send Telegram Notification** nodes require credentials not yet configured in the n8n instance. Both were safely pinned with realistic output data during the safe test. End-to-end logic (field flow, node chaining, log output) was verified independently of external services.

**Action required before live test:** Configure `Google Sheets OAuth2` and `Telegram Bot` credentials in the n8n UI, update the spreadsheet ID and chat ID placeholders, then re-run in live execution mode.

---

## Edge Cases Tested

| Scenario | Input | Expected | Actual | Pass? |
|---|---|---|---|
| Missing `name` field | `body.name` omitted | Falls back to `'N/A'` | `'N/A'` | ✅ |
| Mixed-case field keys | `body.Name` instead of `body.name` | Extracted correctly | Extracted correctly | ✅ |
| Timestamp absent | `body.timestamp` omitted | Falls back to `$now` | `$now` evaluated | ✅ |

---

## Test Environment
- **Mode:** Safe (pin data)
- **Tested by:** Claude (automated)
- **Test date:** 2026-05-22
- **n8n Workflow ID:** tpHlIsVmaSBf1R5b
- **Execution ID:** 33204
- **Instance:** fulcrumtest.app.n8n.cloud
