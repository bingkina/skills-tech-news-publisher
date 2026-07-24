# Image Workflow

Each article needs one generated 5:2 cover immediately after the blockquote summary, with no blank line between the blockquote and the image. Generate it from the finalized article with built-in `image_gen` (Image 2). If the body discusses an A-grade data chart, also add that chart near the paragraph it supports by following **Handle Data Charts** below. Generation and chart capture are automatic; every upload still requires explicit user confirmation. Every Markdown image alt/name must be specific to the article topic and useful for SEO; do not use generic `配图`. The 5:2 ratio applies only to the cover, not to inline data charts.

The live rules in `SKILL.md` and this file override old conversation memory, old workflow summaries, and generic `imagegen` examples. Never copy a generic `no text` or `no logos` constraint into an article-cover prompt unless the user explicitly requests it or the finalized article provides no accurate text or confirmed brand mark to use.

## Build The Prompt

Generate the cover only after the title, summary, and body are finalized. Build the prompt from:

1. The article title.
2. The summary.
3. Three to five A-grade confirmed facts that can be represented visually.
4. The central user-facing idea: what the product or event lets people do.

Do not include B/C-grade claims, rumors, unknown features, speculative impact, or information gaps. If an exact interface, product appearance, chart, number, or logo cannot be confirmed, do not depict it.

Make an explicit editorial choice for text and brand marks instead of silently banning them:

- Title text is allowed. If included, provide the finalized article title verbatim and require exact rendering.
- Finalized-title accuracy is not a title-only rule. Unless the user explicitly requests a title-only cover, do not state, infer, or enforce that all other readable copy must be removed.
- Additional readable copy is allowed when its exact wording is supported by A-grade facts and it does not create a fake interface. Judge it by factual accuracy, not by whether it repeats the title.
- A confirmed brand Logo is allowed when the brand identity is supported by A-grade evidence. Require an accurate, undistorted mark.
- Do not add `no text`, `no logo`, `no logos`, `无文字`, or `无品牌标志` as a default safety constraint.
- Style title typography from the image composition and palette. Use a readable dark neutral base plus one or two restrained image-derived or brand-derived accent colors for key entities, actions, or status phrases; do not render the whole title as a monotonous pure-black line by default.
- Keep title color hierarchy suitable for thumbnail reading. Avoid rainbow coloring, neon accents, low contrast, heavy outlines, and decoration unrelated to the image.
- If one claim or mark is inaccurate, correct only that element. Do not remove all other accurate text or confirmed branding unless the user requests a text-free or brand-free image.

Use this prompt structure:

```text
Use case: stylized-concept
Asset type: Chinese technology news article cover
Primary request: create a visual cover for “<article title>” based on <confirmed subject and user-facing change>
Subject: <concrete objects or scene supported by the article>
Style/medium: clean editorial technology illustration, polished and approachable
Composition/framing: exact 5:2 wide landscape canvas, clear focal point, readable at thumbnail size
Lighting/mood: bright, clear, confident, not dramatic
Color palette: modern restrained technology colors with good contrast
Title text (verbatim): "<finalized article title>" if title text is used; otherwise state the editorial reason for omitting it
Additional copy (verbatim): "<exact A-grade-supported copy and its visual purpose>" if additional readable copy is used; otherwise omit this line
Typography: derive a restrained hierarchy from the image palette; use a dark neutral base and 1–2 coordinated accent colors for key words or status; preserve exact text and thumbnail readability; avoid a flat all-black title
Brand marks: <confirmed brand Logo and required accuracy> if used; otherwise omit this line
Constraints: use only confirmed article details; no watermark, no fake UI, no inaccurate text, no distorted or unverified brand marks, no unsupported product details or numbers
Avoid: dark neon stock imagery, generic circuit-board backgrounds, visual clutter, hype, science-fiction elements unrelated to the article
```

## Generate And Save

Use built-in `image_gen` (Image 2) by default for the cover. Do not search for or download official screenshots, launch-blog images, OpenGraph images, press-kit assets, or stock images as cover substitutes. An original data-chart screenshot required by **Handle Data Charts** is the only default exception.

A verified official Logo asset used only as a targeted edit reference is not a cover substitute. When a confirmed brand Logo needs correction, obtain the reference from the brand's official website or official brand resources; do not use an unverified third-party redraw.

Generate exactly one cover before the first user preview. Inspect it for subject relevance, factual consistency, composition, the accuracy of any included title text, additional readable copy, or logos, fake interfaces, unsupported details, and an exact 5:2 canvas ratio. Verify the actual pixel dimensions before preview or upload (for example, 2000×800). If the ratio is wrong, crop or extend the canvas locally only when the title, Logo, and focal subject remain intact. Never stretch or squeeze the image to force the ratio.

If the first result fails any check, save and show that first result, identify the specific issue, and wait for explicit user approval before making any correction, edit, or regeneration. Do not issue a second `image_gen` call automatically, including for a wrong ratio, misspelled title, inaccurate copy, distorted Logo, weak composition, or generic `imagegen` guidance to iterate after validation. A second image-generation call is allowed only after the user clearly requests a revision or regeneration.

After the user explicitly requests a correction, treat it as a minimal edit:

- If generated text contains an unsupported claim, remove or replace that claim only.
- Do not remove accurate A-grade-supported copy merely because it is not the article title. If unsupported panel copy must be removed, replace it with confirmed wording or clearly non-text visual elements, not abstract glyphs, pseudo-text, or decorative gibberish.
- If title text is misspelled, correct the title text while preserving accurate visual elements.
- If the title is accurate but visually flat or entirely black, edit only its typography, color hierarchy, weight, spacing, or subtle accents to match the image; preserve the exact title and every other accurate element.
- If a confirmed brand Logo is distorted, first use a verified official Logo reference for a targeted edit and re-check its shape, spelling, proportions, and brand identity. Do not replace it with a neutral or unbranded icon merely because the first generation was distorted.
- Only if the reference-guided correction still fails the accuracy check may you remove that Logo or replace only that Logo with a neutral, unbranded icon. If the mark itself is unverified, remove only that mark rather than attempting to preserve it.
- Do not turn a targeted correction into a blanket text-free and brand-free redesign unless the user explicitly requests it.

Copy the selected generated file out of the default generated-images location and save it to the user's Desktop with a stable descriptive name:

```text
~/Desktop/<article-slug>-cover.png
```

Do not leave the selected project asset only in the generator's default storage. Show the generated image and local path when asking whether to upload it.

Avoid:

- Dark, blurred, stock-like atmospheric images.
- Fake UI screenshots.
- Unverified product appearance, features, benchmark numbers, or charts.
- Watermarks, inaccurate text, and unverified or distorted brand marks.
- Decorative robots, holograms, circuit boards, or code rain unrelated to the article.

## Handle Data Charts

When the article discusses an A-grade data chart, capture the original chart and insert it next to the paragraph that explains it. Do not add charts merely as decoration.

1. Open the authoritative source page or PDF and capture only the relevant chart.
2. Crop surrounding navigation and unrelated content, but preserve the chart title, axes, legends, units, labels, data points, and any necessary source mark already present in the original.
3. Save the screenshot to a stable local path and inspect it at the article's actual display width. Treat labels, ticks, or values that cannot be read without opening the original-size file as unclear.
4. If the screenshot is clear, use it. Do not regenerate a clear chart.
5. If it is unclear, use `image_gen` (Image 2) to recreate the chart from the screenshot and the separately verified A-grade data. Specify the exact chart type, title, axis labels, legend, units, and every value. Require a small `根据 <来源> 数据重制` attribution.
6. Compare every label and value in the result against the verified source. Make targeted corrections for any mismatch. If the result still contains wrong text, wrong values, missing data, or misleading visual proportions, do not use it; report the failure and insert `待补图`.

Example body placement:

```markdown
## <正文小节>

<解释图表所支持的已确认结论。>

![<指标名称 + 对比范围 + 图表类型>](<chart-url>)
```

The original source mark inside a screenshot or the required attribution on a recreated chart is an integrity label, not a prose source list. Do not remove it to satisfy the article's no-source-list writing rule.

## Confirm Before Upload

Before running any upload command, ask the user for explicit approval with previews and local paths for the cover and any inline charts.

Every selected cover or chart file must be on the user's Desktop before this confirmation step. Generating or capturing, saving, and previewing an image do not count as upload approval.

Acceptable approvals include clear replies such as:

- `是`
- `确认`
- `上传`
- `yes`
- `用这张`

If the user does not approve, do not upload.

If the user explicitly requests a revision, make the requested single change with `image_gen`, preserve the exact 5:2 cover ratio, save a new versioned file such as `<article-slug>-cover-v2.png`, show it, and ask for upload confirmation again. A diagnostic finding alone is not permission to make this second call.

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
