# Image Workflow

Each article needs one generated image immediately after the blockquote summary, with no blank line between the blockquote and the image. Generate it from the finalized article with built-in `image_gen` (Image 2). Generation is automatic; upload still requires explicit user confirmation. The Markdown image alt/name must be specific to the article topic and useful for SEO; do not use generic `配图`.

## Build The Prompt

Generate the cover only after the title, summary, and body are finalized. Build the prompt from:

1. The article title.
2. The summary.
3. Three to five A-grade confirmed facts that can be represented visually.
4. The central user-facing idea: what the product or event lets people do.

Do not include B/C-grade claims, rumors, unknown features, speculative impact, or information gaps. If an exact interface, product appearance, chart, number, or logo cannot be confirmed, do not depict it.

Use this prompt structure:

```text
Use case: stylized-concept
Asset type: Chinese technology news article cover
Primary request: create a visual cover for “<article title>” based on <confirmed subject and user-facing change>
Subject: <concrete objects or scene supported by the article>
Style/medium: clean editorial technology illustration, polished and approachable
Composition/framing: wide landscape cover, clear focal point, readable at thumbnail size
Lighting/mood: bright, clear, confident, not dramatic
Color palette: modern restrained technology colors with good contrast
Constraints: use only confirmed article details; no text, no logos, no watermark, no fake UI, no unsupported product details or numbers
Avoid: dark neon stock imagery, generic circuit-board backgrounds, visual clutter, hype, science-fiction elements unrelated to the article
```

## Generate And Save

Use built-in `image_gen` (Image 2) by default. Do not search for or download official screenshots, launch-blog images, OpenGraph images, press-kit assets, or stock images as substitutes.

Generate one strong cover first. Inspect it for subject relevance, factual consistency, composition, accidental text, logos, fake interfaces, and unsupported details. If it fails, iterate with one targeted correction.

Copy the selected generated file out of the default generated-images location and save it to the user's Desktop with a stable descriptive name:

```text
~/Desktop/<article-slug>-cover.png
```

Do not leave the selected project asset only in the generator's default storage. Show the generated image and local path when asking whether to upload it.

Avoid:

- Dark, blurred, stock-like atmospheric images.
- Fake UI screenshots.
- Unverified product appearance, features, benchmark numbers, or charts.
- In-image titles, captions, logos, brand marks, and watermarks.
- Decorative robots, holograms, circuit boards, or code rain unrelated to the article.

## Confirm Before Upload

Before running any upload command, ask the user for explicit approval with the generated-image preview and local file path.

The local file path must be on the user's Desktop before this confirmation step. Generating, saving, and previewing the image do not count as upload approval.

Acceptable approvals include clear replies such as:

- `是`
- `确认`
- `上传`
- `yes`
- `用这张`

If the user does not approve, do not upload.

If the user requests a revision, make the requested single change with `image_gen`, save a new versioned file such as `<article-slug>-cover-v2.png`, show it, and ask for upload confirmation again.

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

If built-in image generation fails, do not silently replace it with a network image and do not invent a URL. Tell the user that image generation failed and use the same `待补图` placeholder. Only use a CLI/API fallback if the user explicitly requests that path.

## Insert In Draft

The image line must appear immediately after the summary blockquote. Do not leave a blank line between them:

```markdown
> <摘要>
![<文章核心关键词 + 图片内容描述>](https://example.com/image.webp)

## <第一节>
```
