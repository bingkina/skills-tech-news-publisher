# Article Template

Use this file before Stage 2 and Stage 4. Keep the final draft concise, evidence-backed, and ready for Hexo frontmatter updates.

## Working Article Shape

```markdown
# 标题：<动词 + 核心事实>

> <80-140 字摘要。先给结论，再给关键数字或可信度边界。>
![<文章核心关键词 + 图片内容描述>](<cover-url>)

## <核心事实 1>

<正文内容由 article-writing skill 基于已收集信息生成。写成科技博主的完整文章，而不是新闻摘抄或信源转述。先写核心事实、技术变化、发布时间、价格、benchmark、上下文窗口、开源状态等；信息没有可靠依据就不要写。>

## <核心事实 2>

<继续由 article-writing skill 展开。解释它为什么值得读者关心。优先写具体约束：谁能用、成本多少、限制是什么、和上一代差异在哪里。不要写“根据某媒体/某公司博客/某新闻稿”。>

## <可信度边界>

<由 article-writing skill 根据可信度边界收束。不要点名信息源；可以写“目前还缺少独立评测/复现”“关键参数仍待实测”，把不确定性写成读者可理解的判断。>

```

Frontmatter、blockquote 摘要和图片 Markdown 行的生成逻辑保持不变。正文段落使用 `article-writing` skill 根据 Stage 1 收集到的信息生成，不得改写模板区块，也不得补可靠信息之外的事实。

正文禁止出现信息源名称、来源列表或来源转述句式，例如“根据 X 新闻”“据 X 报道”“X 博客称”“官方公告显示”。不要在正文生成 `## 来源引用 (Sources)` 段；信源只用于内部校验和最终交付给用户，不写进文章主体。

Stage 3 writes the article into `source/_drafts/<slug>.md` and removes the `# 标题：...` line from the saved draft. If a legacy generation accidentally includes `## 来源引用 (Sources)`, remove that whole section before saving.

## Title Rules

- Use a verb plus the core fact.
- Avoid questions unless the news itself is a question.
- Avoid hype words such as `震惊`, `炸裂`, `史诗级`, `王炸`, `颠覆性`.
- Prefer concrete nouns: model name, company name, benchmark, price, release channel.

Examples:

- `某公司发布 Alpha 模型，API 价格保持不变`
- `阿里开源 QoderWork，定位代码智能体工作台`
- `Google 推出 Gemini 3.5 Flash，主打低延迟多模态`

## Hexo Frontmatter Example

Keep `title`, `date`, and `cover` if Hexo already generated them. Add or replace only the SEO fields.

```yaml
---
title: 某公司发布 Alpha 模型，API 价格保持不变
date: 2026-05-30 10:30:00
permalink: posts/2026/05/alpha-model-api-pricing/
categories:
  - AI资讯
tags:
  - Alpha 模型
  - API
  - 大模型
description: 某公司发布 Alpha 模型，API 价格保持不变。本文梳理官方参数、可用渠道、定价变化和第三方评测缺口。
---
```

## Permalink Rules

- Format: `posts/YYYY/MM/<slug>/`
- Use lowercase English words and hyphens.
- Keep the slug short, usually 3-7 words.
- Include the primary searchable entity.
- Remove stop words such as `a`, `the`, `of`, `for`, `to`, `and`.

Good:

- `posts/2026/05/alpha-model-api-pricing/`
- `posts/2026/05/alibaba-qoderwork-code-agent/`
- `posts/2026/05/google-gemini-35-flash/`

Avoid:

- `posts/2026/05/a-new-era-of-ai-models/`
- `posts/2026/05/shocking-openai-release/`
- `Alpha 模型发布`
