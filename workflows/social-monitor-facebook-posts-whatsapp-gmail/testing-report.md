# testing-report.md — Social - Monitor Facebook Posts - WhatsApp & Gmail

## Summary
| Test Type | Result |
|---|---|
| Happy path (success scenario) | ⏳ Pending — credentials not yet configured |
| Induced error (failure handling) | ⏳ Pending — credentials not yet configured |
| Notification path verification | ⏳ Pending — credentials not yet configured |
| Edge cases | ⏳ Pending — credentials not yet configured |

> ⚠️ **Testing Deferred — Credential Configuration Required**
> This workflow was submitted prior to credential configuration in n8n. The workflow logic,
> node graph, and expressions have been reviewed and validated at build time. Full end-to-end
> testing is pending setup of the following credentials in the n8n instance:
> - Facebook Graph App (Facebook Developer Console)
> - WhatsApp Business Cloud API (Meta Business Suite)
> - Gmail OAuth2 (Google Cloud Console)
>
> The reviewer should confirm credentials are configured and a live test is run before approving this PR.

---

## Happy Path Test

**Input used:** N/A — pending credential setup

**Node-by-node results:**
| Node | Status | Output Summary |
|---|---|---|
| Facebook Page Post Trigger | ⏳ Pending | Awaiting Facebook Graph App credential |
| WhatsApp Notify | ⏳ Pending | Awaiting WhatsApp Business Cloud credential |
| Gmail Notify | ⏳ Pending | Awaiting Gmail OAuth2 credential |

**Overall outcome:** Not yet executed — credential configuration required before live test.

---

## Induced Error Test

**Error triggered:** Not yet tested
**Expected behaviour:** Workflow should surface credential/API errors in the n8n execution log
**Actual behaviour:** ⏳ Pending
**Error handling node:** No dedicated error handler node — errors will surface in n8n execution log

---

## Notification Path Verification

**Notification triggered:** ⏳ Pending
**Channel / destination:** WhatsApp (configured recipient number) + Gmail (configured recipient email)
**Message received:** ⏳ Pending

---

## Edge Cases Tested

| Scenario | Input | Expected | Actual | Pass? |
|---|---|---|---|---|
| Post with no message/caption | `message: null` | Falls back to "(no caption)" | ⏳ Pending | ⏳ |
| Post with no post_id | `post_id: null` | Link renders as `https://facebook.com/` | ⏳ Pending | ⏳ |
| Unknown item type | `item: "photo"` | Subject line shows item type correctly | ⏳ Pending | ⏳ |

---

## Test Environment
- **Mode:** Not yet executed
- **Tested by:** Pending
- **Test date:** 2026-05-29 (submission date)
- **n8n Workflow ID:** Wt30C2kiaMCvXCqX
- **Registry ID:** 982d2af0-70cc-436b-963b-f8a0385bceed
- **Instance:** fulcrumtest.app.n8n.cloud
