# Image Workflow

Each article needs one image immediately after the blockquote summary. Do not upload or claim an image URL before user confirmation.

## Pick The Image

Prefer images in this order:

1. Official product screenshot, model card image, launch blog image, GitHub/OpenGraph image, or press kit asset.
2. User-provided local image path.
3. A neutral generated/placeholder image only if no real product image exists and the user accepts it.

Avoid:

- Dark, blurred, stock-like atmospheric images.
- Fake UI screenshots.
- Cropped images that hide the actual product or interface.
- Logos stretched into article covers.

## Confirm Before Upload

Before running any upload command, ask the user for explicit approval with the local file path or source image URL.

Acceptable approvals include clear replies such as:

- `是`
- `确认`
- `上传`
- `yes`
- `用这张`

If the user does not approve, do not upload.

## Upload

Use the image upload mechanism available in the user's blog environment. If the local environment provides an `image` CLI, the expected pattern is:

```bash
image <local-image-path>
```

After upload, copy the returned URL exactly. Never invent an R2 URL.

If upload fails, tell the user:

```text
配图上传失败，请手动补图。
```

Then continue the draft with a clear placeholder:

```markdown
![配图](待补图)
```

## Insert In Draft

The image line must appear immediately after the summary blockquote:

```markdown
> <摘要>

![配图](https://example.com/image.webp)

## <第一节>
```
