# Home Health App - Project Guidelines

## Design Constraints (Mobile-First)

This app is mobile-first, used by nurses and doctors on phones and
iPads, often one-handed at a patient's bedside. Every UI change must
satisfy:

- **Mobile-first CSS**: base styles target phones (~375px); enhance upward
  with min-width breakpoints at 768px (iPad portrait) and 1024px (iPad
  landscape / desktop)
- **Viewport meta tag required**:
  `<meta name="viewport" content="width=device-width, initial-scale=1">`
- **Phone layout**: single column. Case list and case detail are separate
  screens -- tapping a case navigates to detail with a back button.
  iPad 768px+: restore the side-by-side master-detail layout
- **Touch targets**: minimum 44x44px (buttons, case rows, role/person
  switcher, badges that are tappable)
- **Primary actions** (Approve & sign / Send back / Complete visit) sit in
  a sticky bottom action bar on phones, inside safe-area insets
  (`env(safe-area-inset-bottom)`)
- **Form inputs**: font-size 16px minimum (prevents iOS auto-zoom)
- **No hover-only affordances** -- everything discoverable by touch. Hover
  styles allowed only as enhancement inside `@media (hover: hover)`
- **Modals** become full-screen sheets on phones, centered dialogs on 768px+
- **Photo upload** uses `<input accept="image/*" capture="environment">` so
  phones open the camera directly
- **Role/person switcher** collapses to a compact dropdown or bottom sheet
  on phones
- **Test mentally** at 375x667 (small phone), 390x844 (modern phone),
  820x1180 (iPad) before finishing any UI task
