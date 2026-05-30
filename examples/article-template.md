# Article Template

Use this file before Stage 2 and Stage 4. Keep the final draft concise, source-backed, and ready for Hexo frontmatter updates.

## Working Article Shape

```markdown
# 标题：<动词 + 核心事实>

> <80-140 字摘要。先给结论，再给关键数字或可信度边界。>

![配图](<cover-url>)

## <核心事实 1>

<直接写新闻事实、技术变化、发布时间、价格、benchmark、上下文窗口、开源状态等。没有来源不要写。>

## <核心事实 2>

<解释它为什么值得读者关心。优先写具体约束：谁能用、成本多少、限制是什么、和上一代差异在哪里。>

## <可信度边界>

<如果主要信息来自官方通稿，明确写出“目前信息主要来自官方口径，暂无第三方独立评测/复现”。>

## 来源引用 (Sources)

- <source title>: <url>
- <source title>: <url>
```

Stage 3 writes the article into `source/_drafts/<slug>.md` and removes both the `# 标题：...` line and the whole `## 来源引用 (Sources)` section from the saved draft.

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
