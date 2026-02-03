# Image & Asset Guidelines
## Source Image Workflow (Automated)
All assets are managed via a strict source-to-distribution pipeline.

1.  **Humans** upload original, high-quality images to `images/_source/`.
    *   Do NOT upload directly to `hero`, `gallery`, etc.
    *   Do NOT manually resize or convert to WebP.
2.  **GitHub Action** detects changes, optimizes, generates variants (480/768/1280px + blur), and commits them to the appropriate folders.
3.  **Developers** use the generated URLs in production.

## Developer Workflow
1.  **Step 1:** Upload image (e.g., `my-new-hero-v1.jpg`) to `images/_source/`.
2.  **Step 2:** `git add .` -> `git commit -m "add new hero"` -> `git push`.
3.  **Step 3:** Wait ~1 minute for the Action to run.
4.  **Step 4:** Your images are available at `.../images/hero/my-new-hero-v1-1280.webp` etc.

## Folder Naming Conventions
- **Source:**
  - `images/_source/` -> Default landing spot (routes to `hero` by default).
  - `images/_source/gallery/<project-name>/` -> Routes to `images/gallery/<project-name>/`.
  - `images/_source/logos/` -> Routes to `images/logos/`.

## File Naming Conventions
- **Format:** `[descriptive-name]-v[version].[ext]`
- **Rules:**
  - Use lowercase letters.
  - Use hyphens as separators (no spaces or underscores).
- **Examples:**
  - `hero-main-v1.jpg`
  - `logo-brand-v2.png`

## Versioning Strategy
We use **immutable filenames** for versioning.
- **Do not** overwrite a file in `_source` (the system will skip re-generation if output exists).
- **Do** increment the version number in the filename (e.g., `hero-v1.jpg` -> `hero-v2.jpg`).

### Why?
jsDelivr and other CDNs aggressively cache files based on the URL. Changing the filename forces the browser to fetch the new asset immediately.

## CDN Caching
- **GitHub releases/tags:** jsDelivr caches permanently.
- **Master/Main branch:** jsDelivr caches for shorter periods but relies on file content changes or distinct URLs.

## What NOT to Upload
1.  **Sensitive Data:** Never upload images containing private user info, secrets, or internal documents. This repository is public.
2.  **Temporary Files:** No `DS_Store` or temp drafts.
3.  **Manually Optimized Files:** Do not upload your own WebP files to `_source` unless you want them processed again (not recommended). Upload high-quality sources instead.

---

> **IMPORTANT NOTE:**
> **Never overwrite existing images.** Always modify the filename (increment version) when updating an asset.
> **Never modify the generated folders** (`hero`, `gallery`, `logos`, `placeholders`) manually. They are managed by the bot.
