# testing-report.md — Monitoring - Alert Failed Transactions - Microsoft Teams

## Summary
| Test Type | Result |
|---|---|
| Happy path (success scenario) | ⚠️ Not run — demo workflow with placeholder credentials |
| Induced error (failure handling) | ⚠️ Not run — demo workflow with placeholder credentials |
| Notification path verification | ⚠️ Not run — demo workflow with placeholder credentials |
| Edge cases | ⚠️ Not run — demo workflow with placeholder credentials |

---

## Note on Test Status
This workflow was submitted as a **demo / skeleton** with placeholder credentials (`YOUR_TEAM_ID`, `YOUR_CHANNEL_ID`) and no live PostgreSQL connection configured. Full integration testing must be completed by the admin reviewer before this workflow is activated in production.

**Required before activation:**
1. Assign the `PostgreSQL - Production DB` credential in the `Get Failed Transactions` node
2. Replace `YOUR_TEAM_ID` and `YOUR_CHANNEL_ID` in the `Send Teams Alert` node with real values
3. Run a safe pin-data test via the n8n-workflow-tester skill
4. Run a live manual execution against a staging/test DB to confirm end-to-end Teams delivery

---

## Happy Path Test

**Input used:** Not executed — placeholder credentials prevent live test

**Expected node-by-node behaviour:**
| Node | Expected Status | Expected Output |
|---|---|---|
| Every 5 Minutes | ✅ Fires on schedule | Timestamp item |
| Get Failed Transactions | ✅ Returns 0..N rows | Rows with id, transaction_id, amount, currency, status, error_code, error_message, created_at, account_id |
| Format Alert Message | ✅ Runs once per row | teamsMessage, transaction_id, amount, error_code, failed_at fields |
| Send Teams Alert | ✅ Posts HTML card | 201 response from Teams Graph API |

---

## Induced Error Test

**Error triggered:** Not executed
**Expected behaviour:** If PostgreSQL is unreachable, the workflow execution errors at `Get Failed Transactions` and the error is surfaced in the n8n execution log
**Actual behaviour:** Not verified
**Note:** Consider adding an error handler node to send a Teams alert if the DB query itself fails

---

## Notification Path Verification

**Notification triggered:** Not verified
**Channel / destination:** Microsoft Teams — team and channel IDs to be configured
**Message received:** Not verified

---

## Edge Cases Tested

| Scenario | Input | Expected | Actual | Pass? |
|---|---|---|---|---|
| No failed transactions in window | 0 rows returned | Workflow silently no-ops (correct polling behaviour) | Not verified | ⚠️ |
| Multiple failures at once | N rows returned | N separate Teams messages posted | Not verified | ⚠️ |
| DB connection timeout | Unreachable host | Execution errors at Postgres node | Not verified | ⚠️ |

---

## Test Environment
- **Mode:** Not run — demo submission
- **Tested by:** N/A
- **Test date:** 2026-05-29
- **n8n Workflow ID:** AYp70kHaSYW80jus
- **Registry ID:** 05ae8698-435b-442d-8eb4-530e256a463a
- **Instance:** fulcrumtest.app.n8n.cloud
