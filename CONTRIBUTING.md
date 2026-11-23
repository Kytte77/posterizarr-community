# Contributing to Posterizarr Community Gallery

Thank you for sharing your Posterizarr style or overlay setup! You can submit everything **directly in the GitHub web UI** — no local Python, Git CLI, or manual `index.json` editing required.

## Folder & Naming Rules

- **Blueprints:** `blueprints/<your-github-username>/` *(or `blueprints/<your-github-username>/<preset-slug>/` if you share more than one style)*
- **Dynamic Overlays:** `dynamic-overlays/<your-github-username>/` *(or `dynamic-overlays/<your-github-username>/<bundle-slug>/` if you share more than one bundle)*
- Use your exported filename directly — both `custom_blueprint.json` / `blueprint.json` and `posterizarr-overlays.zip` / `bundle.zip` work out of the box.
- Drop **1–4 preview screenshots** (`.jpg`, `.jpeg`, `.png`, or `.webp`, max `2 MiB` each) into the same folder — they are detected automatically!
- Do **not** edit `index.json` manually — GitHub Actions rebuilds it automatically on merge.

## Minimal `meta.json`

Only `name` and `description` are required:

```json
{
  "name": "My Clean Clearlogo Style",
  "description": "Minimalist black borders with flat white clearlogos and crisp episode title cards."
}
```

### Optional Fields

If you want extra details or custom preview order, you can add any of these:

```json
{
  "name": "My Clean Clearlogo Style",
  "description": "Minimalist black borders with flat white clearlogos and crisp episode title cards.",
  "tags": ["clearlogo", "minimal", "borders"],
  "previews": ["preview-movie.jpg", "preview-show.jpg"],
  "author": "your-github-username",
  "author_url": "https://github.com/your-github-username",
  "source_url": "https://github.com/optional/upstream-reference",
  "min_posterizarr_version": "4.0.0",
  "notes": "Optional tips, required fonts, or extra notes shown in the UI."
}
```

| Field | Required | Default / Rules |
|---|---|---|
| `name` | Yes | String, `2–80` characters |
| `description` | Yes | String, `10–400` characters |
| `tags` | No | Defaults to `[]`; up to `8` lowercase tags (`^[a-z0-9][a-z0-9-]{0,29}$`) |
| `previews` | No | Auto-discovers up to `4` images in the folder if omitted; `1–4` relative filenames (max `2 MiB` each) |
| `author` | No | Defaults to your folder name (`<your-github-username>`) |
| `author_url` | No | Defaults to `https://github.com/<your-github-username>`; must start with `https://` |
| `source_url` | No | Optional `https://...` attribution link |
| `min_posterizarr_version` | No | Defaults to `"4.0.0"` |
| `notes` | No | Optional string up to `500` characters |

## Automated Safety Checks (GitHub Actions)

When you open a Pull Request, GitHub automatically verifies:
- **Blueprints:** max `256 KiB`, valid JSON, visual settings only (no server URLs, API keys, webhooks, or local file paths).
- **Dynamic Overlays:** valid Posterizarr export bundle (`posterizarr-overlay-bundle` v1), max `20 MiB`, valid checksums, and no leaked credentials or LAN URLs.

*(Maintainers / developers testing locally can optionally run `python scripts/validate_and_index.py --strict`.)*
