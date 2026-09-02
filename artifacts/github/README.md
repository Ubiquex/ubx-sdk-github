# artifacts/github

UBI-240 slice 6: the canonical home for this provider's own docs/codegen
artifacts, moved here from `ubiquex-docs`. See `ubx-sdk-kubernetes`'s
own `artifacts/kubernetes/README.md` for the full account of why this
moved (UBI-102's own comment thread) and how the four files divide.

- **`descriptions.json`** / **`intros.json`** / **`categories.json`** /
  **`exclusions.json`** — real source of truth, read by
  `ubx-docs-providers` at build time.
- **`github.json`** — codegen-ready export (`{resource: {relPath:
  text}}`, qualifier-stripped, HTML-unescaped). What `ubx sdk gen
  --descriptions-dir artifacts/github` actually reads. Never edited
  directly.

To update: edit `descriptions.json` here, then regenerate `github.json`
from a sibling `ubiquex-docs` checkout:

```bash
ubx sdk gen --only github --dump-ir /tmp/dump --out /tmp/unused
cd ~/Ubiquex/ubiquex-docs/scripts/resource-reference-gen
python3 export_raw_descriptions.py github GitHub \
    --dump-root /tmp/dump/github \
    --descriptions-path ~/Ubiquex/ubx-sdk-github/artifacts/github/descriptions.json \
    --nested-out ~/Ubiquex/ubx-sdk-github/artifacts/github/github.json
```

Commit both files together.
