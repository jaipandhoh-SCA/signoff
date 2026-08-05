# Signoff — Project Notes

Working log for taking signoff-prototype.html to Claude Code.
Source docs: SOP-referral-approval.md, signoff-prototype.html

---

## Feature Roadmap

| # | Feature | SOP ref | Status |
|---|---------|---------|--------|
| 1 | Append-only event history | §7 | Done |
| 2 | Revise & resubmit flow (restart at send-back stage) | §5.3 | Not started |
| 3 | Attachments + wound-photo rule | §5.1 | Not started |
| 4 | Stalled-case timers & flags | §5.4 | Not started |
| 5 | Persistence / backend | §7, §10 | Not started |
| 6 | Notifications | §8 | Not started |

---

## Feature 1: Append-Only Event History

**Why first:** Prototype mutates stages in place — `resubmitStage` erases
rejections, violating §7 ("sign-offs are permanent, send-backs stay visible").
Everything else builds on the data model, so fix it before adding features.

**The change:** Store events (signoff, sendback, resubmit, escalated) in an
immutable log per case. Stage status is derived from events, never stored.
Timeline UI gains full history per stage (sent back → resubmitted → approved).

**Claude Code prompt:**

```
Read SOP-referral-approval.md and signoff-prototype.html. Refactor the
prototype's data model from mutable stage objects to an append-only
event log, per SOP Section 7:

- Each case holds an immutable array of events: {type: 'created' |
  'signoff' | 'sendback' | 'resubmit' | 'escalated', role, actorCode,
  timestamp, note, chainLine, stageIndex}
- Current stage status is DERIVED from the event log, never stored/edited
- Fix resubmitStage: a resubmission appends a 'resubmit' event; the prior
  sendback event and its reason remain permanently visible in the timeline
- Per SOP 5.3, resubmission restarts the chain at the stage that issued
  the send-back; earlier approvals stay valid
- Render full case history in the detail timeline, including past
  send-backs/resubmits, not just current stage states
- Keep all existing UI/UX and styling identical otherwise
```

---

## Decisions Log

- 2026-07-15 — Feature order set. Append-only history first (biggest
  architectural gap; avoids rewriting later features).
- 2026-07-15 — Feature 1 complete. Prototype already uses append-only
  event log: status derived via stageStatus(), resubmit preserves
  sendback history, earlier approvals survive per SOP 5.3.

## Open Questions (from SOP placeholders)

- Does a revision that changes clinical content restart the full chain? (§5.3)
- Escalation clinical criteria — Medical Director to define (§6.1)
- Backup approvers per role (§4)
- Urgent-case pathway (§9)
- Notification channels: in-app vs email/SMS (§8)
