# Image Workflow

Each article needs one image immediately after the blockquote summary, with no blank line between the blockquote and the image. Do not upload or claim an image URL before user confirmation. The Markdown image alt/name must be specific to the article topic and useful for SEO; do not use generic `配图`.

## Pick The Image

Prefer images in this order:

1. Official product screenshot, model card image, launch blog image, GitHub/OpenGraph image, or press kit asset.
2. User-provided local image path.
3. A neutral generated/placeholder image only if no real product image exists and the user accepts it.

If the user explicitly asks you to generate an image, generate a technology-style image whose content matches the article title. Save the generated image to the user's Desktop automatically, then show/mention that local Desktop path when asking whether to upload it.

Avoid:

- Dark, blurred, stock-like atmospheric images.
- Fake UI screenshots.
- Cropped images that hide the actual product or interface.
- Logos stretched into article covers.

## Confirm Before Upload

Before running any upload command, ask the user for explicit approval with the local file path or source image URL.

For generated images, the local file path should be on the user's Desktop before this confirmation step. Generating and saving the image does not count as upload approval.

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
![<文章核心关键词 + 图片内容描述>](待补图)
```

## Insert In Draft

The image line must appear immediately after the summary blockquote. Do not leave a blank line between them:

```markdown
> <摘要>
![<文章核心关键词 + 图片内容描述>](https://example.com/image.webp)

## <第一节>
```
