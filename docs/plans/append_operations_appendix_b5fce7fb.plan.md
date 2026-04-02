---
name: Append Operations Appendix
overview: "Add the \"Appendix: Operations & money\" section to the existing Cabarete marketplace plan file after the \"Risks / constraints\" section, closing the gap between technical design and vendor-platform operations."
todos:
  - id: insert-appendix
    content: Append Operations & money section to cabarete_services_marketplace_e5a6d914.plan.md after Risks / constraints
    status: pending
isProject: false
---

# Append "Operations & money" to plan file

## Target file

- `[/Users/kaiserneptunhuhn/.cursor/plans/cabarete_services_marketplace_e5a6d914.plan.md](/Users/kaiserneptunhuhn/.cursor/plans/cabarete_services_marketplace_e5a6d914.plan.md)`

## Change

Insert a new markdown section **after** the final bullet under **## Risks / constraints** (after the referral/tax line, currently end of file ~line 530). Append:

1. Horizontal rule `---` (optional separator before appendix)
2. `**## Appendix: Operations & money (product + ops)`** with subsections:
  - **Purpose** (one short paragraph)
  - **A. Creem confirmation** — checklist: charge model, split/payout, refund webhooks, reporting (confirm before build commitments)
  - **B. Payout cadence** — table: accounting truth, vendor-visible balance, weekly default cadence, minimum payout floor, failure handling
  - **C. Refund matrix** — table: scenarios (customer cancel, no-show, chargeback, wrong amount, referral dispute) with initiator, owner, system actions; rule that financial state is webhook/admin-audited only
  - **D. Disputes** — tier table (policy → vendor-customer → admin → superadmin) + automation note for auto-refund within policy
  - **E. Minimum notification events** — bullets for Vendor / Customer / Staff (aligned with prior assistant draft)
  - **F. Open items** — workshop items (cancellation windows, currency, tax wording)

Use the full prose from the prior assistant message in this thread (the "ready-to-paste" appendix), ensuring tables render as valid GitHub-flavored markdown.

## Frontmatter (optional)

If you want traceability in todos, add one line to the YAML `overview` or a new todo `operations-appendix` — **optional**; the user only asked for the appendix body.

## Verification

- Open the plan in the editor and confirm the appendix appears after **Risks / constraints** with no broken heading hierarchy (`##` for appendix, `###` for lettered subsections).

