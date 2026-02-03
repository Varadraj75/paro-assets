# Paro Assets

## Purpose
This repository serves as a centralized, production-ready storage for static image assets used in the startup website. It is designed to host optimized images that are served via a global CDN.

## GitHub + jsDelivr
We use GitHub in combination with jsDelivr to provide a zero-cost, high-performance Content Delivery Network (CDN) for our assets.
- **Reliability:** GitHub stores the versioned history of every asset.
- **Performance:** jsDelivr caches files globally, ensuring fast load times for users anywhere.
- **Cost:** Free and vendor-neutral.

## Base CDN URL
To access files, use the following URL pattern:
`https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/`

**Example:**
If you upload `images/hero/hero-v1.webp`, the URL will be:
`https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1.webp`

## Automated Optimization Workflow
We utilize GitHub Actions to automatically optimize and version our assets.

**The Workflow:**
1.  **Upload** high-quality originals to `images/_source/`.
2.  **Commit & Push** your changes.
3.  **Wait** for the "Image Optimization" action to complete.
4.  **Use** the automatically generated URLs from the `hero`, `gallery`, or `logos` folders.

> **Note:** The `images/_source/` folder is strictly for inputs. Never use these raw files in your application. Always use the optimized versions from the destination folders.

## Base CDN URL
To access files, use the following URL pattern:
`https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/`

**Example:**
If you upload `hero-v1.jpg` to `images/_source/`, the system generates:
- `images/hero/hero-v1-480.webp`
- `images/hero/hero-v1-768.webp`
- `images/hero/hero-v1-1280.webp`
- `images/hero/hero-v1-blur.webp`

URL: `https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-1280.webp`

## Image Preparation Rules
Even with automation, follow these source rules:
1.  **Format:** Upload highest quality `.jpg` or `.png`.
2.  **Naming:** Use **versioned filenames** (e.g., `hero-v1.jpg`).
3.  **Organization:**
    - Place galleries in `images/_source/gallery/<project-name>/`.
    - Place logos in `images/_source/logos/` (or prefix with `logo-`).
    - Everything else goes to `images/_source/` (defaults to `hero`).

## Usage Example
Use `srcset` for responsive images and always include `loading="lazy"` for off-screen images.

```html
<img
  src="https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-480.webp"
  srcset="
    https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-480.webp 480w,
    https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-768.webp 768w,
    https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-1280.webp 1280w
  "
  sizes="(max-width: 600px) 480px, (max-width: 900px) 768px, 1280px"
  alt="Description of image"
  loading="lazy"
  width="1280"
  height="720"
  style="background-image: url('https://cdn.jsdelivr.net/gh/Varadraj75/paro-assets/images/hero/hero-v1-blur.webp'); background-size: cover;"
>
```