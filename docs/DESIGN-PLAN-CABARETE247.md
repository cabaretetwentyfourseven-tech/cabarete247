# Cabarete247 — Responsive design plan (mobile-first)

This document is the **authoritative UI specification** for the Quasar/Vue app. **Mobile is the default and primary surface**; tablet and desktop are **progressive enhancements** of the same layouts—not separate “desktop sites.”

When the codebase lives in the `cabarete247` repository, **copy or move this file** into `docs/DESIGN-PLAN.md` (or keep as root `DESIGN-PLAN-CABARETE247.md`) so it ships with the project.

---

## 1. Principles

1. **Mobile-first, first, first** — Design and review at **375×812** (iPhone SE / 13 mini) before any larger breakpoint. If it fails on mobile, it is not done.
2. **One column by default** — No multi-column grids below `md`. Staff dashboards use **stacked sections**; widen to **two columns** only at `lg+` where it reduces scrolling without hiding actions.
3. **Thumb zone** — Primary actions in the **bottom half** of the screen where possible (FAB, sticky footer CTA, Quasar `QPageSticky`).
4. **Touch, not hover** — No hover-only affordances. Tap targets **≥ 44×44 px** (Apple HIG); prefer **48px** for primary CTAs.
5. **Progressive disclosure** — Beach path stays minimal; advanced filters and staff tables stay behind **expand** / **second screen**, not dense above-the-fold chrome.
6. **Readable in sun** — Contrast and large type beat decoration; support **prefers-color-scheme** and optional **high-contrast** Quasar theme toggle later.

---

## 2. Breakpoints (align with Quasar)

Use Quasar’s default `$breakpoint` names so components and `useQuasar().screen` stay consistent:

| Name | Min width | Role |
| --- | --- | --- |
| **xs** | 0–599px | **Primary design target** — all public + vendor flows. |
| **sm** | 600–1023px | Large phones landscape, small tablets; still mostly single column. |
| **md** | 1024–1439px | Tablet / small laptop; staff may use **two-column** shell (nav + content). |
| **lg+** | 1440px+ | Optional side drawer always visible for **admin**; never required for core tasks. |

**Rule:** Ship v1 with **no** layout that requires `md` to complete a booking or show QR.

---

## 3. Layout shells by role

### 3.1 Public (tourist)

- **Header**: minimal — logo + optional language; **no** persistent nav clutter.
- **Content**: single column; offer **cards** full width with consistent padding `16px` horizontal (`px-md` 24px on sm+ if desired).
- **Footer**: optional; keep thin on mobile.
- **Sticky**: one primary CTA per step (“Continue”, “Pay”) — `QPageSticky` position bottom, safe-area aware.

### 3.2 Vendor (`/vendor/*`)

- **Bottom navigation** (Quasar `QFooter` + `QTabs` or `QRouteTab`): **Home** (QR + today) | **Listings** | **Bookings** | **Profile** — **4 tabs max** to preserve thumb reach.
- **QR screen**: **full viewport**; hide chrome or use minimal top bar “Done”.
- **No** hamburger-only primary nav on mobile for vendor — tabs are faster.

### 3.3 Curator / Admin / Superadmin (`/curator/*`, `/admin/*`, `/superadmin/*`)

- **Mobile**: **single column**; **left drawer** for section nav (Quasar `QLayout` drawer) triggered by **menu icon** top-left; **no** permanent sidebar on xs.
- **md+**: optional **split**: fixed mini-drawer + main content.
- **Data-heavy views** (ledger, reports): **card list** per row on mobile; **table** only from `md+` **or** horizontal scroll with **sticky first column** if unavoidable (prefer cards).

---

## 4. Typography

| Token | Mobile (xs) | sm+ |
| --- | --- | --- |
| **Page title** | `text-h5` / 22px bold | `text-h4` |
| **Section title** | `text-subtitle1` / 16px semibold | same |
| **Body** | `text-body1` / 16px — **never below 14px** for primary content | same |
| **Caption / meta** | `text-caption` / 12–13px | same |

Use **line-height ≥ 1.4** for body. **Avoid** all-caps blocks except short badges.

---

## 5. Spacing and grid

- **Page padding**: `16px` horizontal on xs; `24px` from sm optional.
- **Vertical rhythm**: section gaps `24px`; between related controls `12px`.
- **Cards**: `border-radius` consistent (e.g. Quasar default `rounded-borders`); internal padding `16px`.

---

## 6. Components (Quasar-first)

| Need | Component | Mobile note |
| --- | --- | --- |
| Primary action | `QBtn` color=primary, unelevated or flat | Full width on narrow screens for checkout steps |
| Secondary | `QBtn` outline / flat | Same min height 48px |
| Lists | `QList` + `QItem` | Booking rows; swipe actions optional later |
| Forms | `QInput`, `QSelect` with `stack-label` or `outlined` | `dense` only if touch target still ≥ 44px total |
| Feedback | `QBanner`, `QLinearProgress` | Skeleton loaders for storefront |
| QR | `Qrcode` or canvas; wrapper with **padding + bg** for contrast | Fullscreen page variant |
| Media embeds | Aspect ratio container `16/9`; **max-height** on mobile | Lazy load |

---

## 7. QR and beach-specific patterns

- **Fullscreen QR**: `100dvh`, dark or light theme with **high contrast**; **“Copy link”** + **Share** (Web Share API) below code.
- **Sun / glare**: Offer **invert** or **thick module border** toggle (stored in `localStorage`).
- **Wet hands**: Large hit areas; avoid tiny icon-only buttons without labels for critical paths.

---

## 8. Staff tables and finance (mobile)

- **Never** require horizontal scroll for **primary action** (e.g. “Approve”).
- Pattern: **summary card** per vendor or per day with **tap → detail** drill-down.
- **Export** (CSV): button in **admin** toolbar; same placement mobile/desktop.

---

## 9. Accessibility (baseline)

- **Focus**: visible focus rings on interactive elements (Quasar focusable).
- **Labels**: all inputs have associated labels; icons have `aria-label`.
- **Motion**: respect `prefers-reduced-motion` for large transitions.
- **Color**: do not rely on color alone for status — add icon or text (“Paid”, “Pending”).

---

## 10. Storybook / visual QA

- **Default viewport**: **375×812** in Storybook (or Ladle) `parameters.viewport.defaultViewport`.
- **Additional**: `iphone12`, `pixel5`, one **tablet** for staff shell.
- **Stories**: one story per **scenario** in the master plan (T-01 … S-02); include **loading** and **error** states.

---

## 11. Responsive checklist (before merge)

- [ ] Tested at **375px** width — no horizontal overflow on key pages.
- [ ] All primary flows completable **without** desktop browser.
- [ ] Touch targets ≥ 44px; sticky CTA does not cover critical content (safe-area).
- [ ] Staff views usable on mobile (drawer + stacked cards).
- [ ] Storybook screenshots captured at mobile for critical components.

---

## 12. File placement in repo

```
cabarete247/
  docs/
    DESIGN-PLAN.md          # optional rename of this document
  src/
    css/
      quasar.variables.scss # breakpoint + brand tokens
```

Keep **brand colors** and **font stacks** in `quasar.variables.scss` (or Quasar v2 theming) so Storybook and app share one source of truth.

---

*End of design plan — mobile-first.*
