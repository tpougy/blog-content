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

## Images

### Regular images

Place image files in `./assets/` next to the article and reference them with a relative path:

```md
![Alt text](./assets/diagram.png)
```

### Theme-aware images (light/dark variants)

Images that should switch between light and dark mode require a different setup:

1. **Place both variants in the frontend repo** at `blog/public/<some-path>/`:
   ```
   blog/public/diagrams/my-image.light.svg
   blog/public/diagrams/my-image.dark.svg
   ```

2. **Reference the image with an absolute path** from the article:
   ```md
   ![Alt text](/diagrams/my-image.light.svg)
   ```

The rehype plugin detects the `.light.` or `.dark.` suffix and generates a `<picture>` element that swaps the image based on the active theme.

> **Why `blog/public/`?** Cloudflare Workers serves both variants as static assets from the same path. If you place them in `./assets/` relative to the post, the derived sibling cannot be resolved at serve time.

## Requirements

- [`uv`](https://docs.astral.sh/uv/) >= 0.9.x installed locally — Python is auto-managed by uv, no separate installation needed.
