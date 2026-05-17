# tpougy.blog — Content

Obsidian vault and content repository for [tpougy.blog](https://tpougy.blog).

## Layout

```
posts/
  en/NN-slug/
    article.md
    assets/
  pt/NN-slug/
    article.md
    assets/
projects/
  en/project-name/index.md
  pt/project-name/index.md
scripts/
  new-post
```

## Writing a new post

Run from the vault root:

```bash
./scripts/new-post "My Article Title"
```

This scaffolds stubs for **both** EN and PT in a single command with an auto-incremented numeric prefix, empty `assets/` directories, and `draft: true` so the post does not appear on the published site until the field is removed or set to `false`.

> **Note:** `uvx new-post "My Article"` does **not** work — `uvx` only runs PyPI-published packages, not local files. Use `./scripts/new-post` (with the execute bit) or `uv run --script scripts/new-post "My Article"` if the execute bit is not set.

## Publishing

Write drafts on the `drafts` branch. When a post is ready to publish:

```bash
git checkout main
git merge drafts
git push origin main
```

Pushing to `main` will (after Phase 4) trigger a Cloudflare Workers production build automatically.

## Requirements

- [`uv`](https://docs.astral.sh/uv/) >= 0.9.x installed locally — Python is auto-managed by uv, no separate installation needed.
