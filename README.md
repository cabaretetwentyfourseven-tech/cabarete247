# Cabarete247

Mobile-first marketplace (Quasar + Vue + Supabase + Creem + GitHub Pages). Planning and design live under **`docs/`**.

## Documentation

| Path | Description |
| --- | --- |
| [`docs/plans/cabarete_services_marketplace_e5a6d914.plan.md`](docs/plans/cabarete_services_marketplace_e5a6d914.plan.md) | Master plan (architecture, phases, appendices A–L) |
| [`docs/plans/append_operations_appendix_b5fce7fb.plan.md`](docs/plans/append_operations_appendix_b5fce7fb.plan.md) | Historical Cursor plan: Operations appendix insertion (superseded by content in master plan) |
| [`docs/DESIGN-PLAN-CABARETE247.md`](docs/DESIGN-PLAN-CABARETE247.md) | Mobile-first responsive UI spec |

## Execution order (summary)

1. Fill **Appendix J** (YES/NO/NUMBER) in the master plan.
2. Complete **Appendix A** Creem sign-off in Dashboard.
3. **M1:** Quasar app in this repo, Supabase project, roles, stub checkout.
4. **M2:** Creem + webhooks + `ledger_lines` + admin/vendor financial views.

## GitHub: first push

`remote: Repository not found` means GitHub **does not have that repo yet** (or your account cannot see it). The URL must exist **before** `git push`.

1. **Create** the empty repository on GitHub (web UI): org **cabaretetwentyfourseven-tech** → **New repository** → name **`cabarete247`** → leave “Initialize with README” **unchecked** (you already have commits locally).
2. Confirm you have **push** access to that org (member or deploy key).
3. Push:

```bash
cd /path/to/CabareteHTML
git push -u origin main
```

If the org or repo name is different, fix the remote:

```bash
git remote set-url origin https://github.com/<org-or-user>/<repo>.git
```

Use **HTTPS + GitHub credential helper** or **SSH** (`git@github.com:org/repo.git`) per your setup.
