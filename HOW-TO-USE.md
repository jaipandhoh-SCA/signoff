# How to Use Signoff

Signoff is a referral and approval-chain tracker for home health and stem cell wound care teams. This guide walks through every feature.

**Live app:** https://jaipandhoh-sca.github.io/signoff/signoff-prototype.html

---

## Switching roles

The app simulates multiple users. Pick a person from the **switcher** at the top:

- **On phone:** tap the dropdown to select a user
- **On iPad/desktop:** click any person pill (initials with role label)

Each person sees the app from their role's perspective. Primary and backup users are available for every role.

---

## The four roles

| Role | What they do |
|------|-------------|
| **Doctor** | Opens new referrals, revises sent-back cases, can escalate to wound care |
| **Head Nurse** | Reviews orders for completeness, checks for wound photos |
| **Head of Staff** | Confirms staffing/scheduling readiness |
| **Nurse** | Performs the initial check-in visit, logs patient visits on active cases |

Approvals must happen in this exact order. A stage is locked until the one before it is approved.

---

## Creating a new referral

1. Switch to any **Doctor** user
2. Tap **+ New referral**
3. Fill in the required fields (marked with *):
   - Patient name
   - Diagnosis / reason for referral
   - Visit frequency (e.g. "3x/week")
   - Order note (care instructions)
4. Optionally check **Wound-related referral** and attach photos
5. Tap **Submit order**

The doctor's submission counts as the first sign-off. The case moves to Head Nurse review.

---

## Approving or sending back

1. Switch to the role that the case is waiting on
2. Select the case from the list (on phone, tap the case row to open detail)
3. Scroll to the active stage — you'll see the action box
4. Add a note (optional for approval, **required** for send-back)
5. Tap **Approve & sign** or **Send back**

On phones, the primary actions also appear in a **sticky bar at the bottom** of the screen.

---

## Revising a sent-back case

1. Switch to a **Doctor** user
2. Open the case that was sent back
3. Tap **Revise & resubmit**
4. Update diagnosis, frequency, order note, or attachments
5. Check "This revision changes clinical content" if the full approval chain should restart
6. Tap **Resubmit**

---

## Wound care escalation

Once a home health approval chain is fully approved:

1. Switch to a **Doctor** or **Head Nurse** user
2. Open the fully-approved case
3. Scroll to the "Home health chain complete" box
4. Tap **Escalate to wound care**

This opens a second approval chain for the wound care business line. The home health history stays attached.

---

## Patient visits (Nurse role)

Once a case is **Active** (all approvals complete), nurses can log visits:

1. Switch to a **Nurse** user
2. Open an active case
3. Scroll to the **Visits** section
4. Tap **Start visit** — this records a clock-in timestamp

**Completing a visit:**
1. Write visit notes in the text area (required — the form won't submit without them)
2. Tap **Complete visit** — this records clock-out, calculates duration, and saves the notes

**Rules:**
- A nurse with an **open visit** on any case cannot start a new visit elsewhere. The case list shows an "Unsubmitted notes" red badge on the blocking case
- If a visit stays open past **4 hours**, it flags as stalled and the Head of Staff is notified
- Visit notes and times are submitted together as one action

**Amendments:**
- Submitted visits cannot be edited, but you can add an **amendment** (correction entry). The original stays visible — append-only, per SOP.

---

## Notifications

Tap the bell icon to see notifications for:
- **Turn** — a case is now waiting on your review
- **Sent back** — a case you submitted was returned (doctors only)
- **Stalled** — a case or visit has exceeded its time threshold (Head of Staff)
- **Active** — all approvals complete, care may begin (Head of Staff)

Tap a notification to jump to that case. Tap **Mark all read** to clear the badge.

---

## Stalled-case timers

Each stage has a target turnaround time. The case list and detail view show colored badges:
- **On time** (green) — within target
- **Overdue** (yellow) — past target but before flag threshold
- **Stalled** (red) — past flag threshold, Head of Staff notified

---

## Exporting audit data

In any case detail, scroll to **Full event history**:
- **Export CSV** — downloads a spreadsheet of all events
- **Export JSON** — downloads a structured JSON file with full attribution and timestamps

---

## Data persistence

- All data (cases, events, visits, attachments, read receipts) is saved to your browser's **localStorage**
- Data survives page reloads and browser restarts
- Tap **Reset demo data** in the footer to clear everything and reload the seed cases
- This is a prototype — do not use for real patient data

---

## Tips for testing

- **On your laptop:** use Chrome DevTools (Cmd+Shift+M) to toggle device mode and test at 375px (phone), 820px (iPad)
- **On your phone:** open the live URL in Safari, then Share > Add to Home Screen for a full-screen experience
- Try the full flow: create a referral as Doctor, approve through each role, then log a visit as Nurse
- Test a send-back: as Head Nurse, send back a case, then switch to Doctor to revise and resubmit
- Test the visit gate: start a visit on one case, then try starting another on a different case
