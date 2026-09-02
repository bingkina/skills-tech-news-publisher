# Article Template

Use this file before Stage 2 and Stage 4. Keep the final draft concise, evidence-backed, and ready for Hexo frontmatter updates.

## Working Article Shape

```markdown
# 标题：<动词 + 核心事实>

> <80-140 字摘要。先说明发生了什么，再给已经确认的关键数字、使用入口或用户影响。不要写任何未确认信息或信息空缺。>
![<文章核心关键词 + 图片内容描述>](<cover-url>)

## <核心事实 1>

<正文内容由 article-writing skill 基于已确认信息生成。写成普通用户能读懂的完整文章，而不是新闻摘抄或信源转述。先说明产品或事件是什么，再写已确认的技术变化、发布时间、价格、使用入口、benchmark、上下文窗口、开源状态等；信息没有可靠依据就整条删除。>

## <核心事实 2>

<继续由 article-writing skill 展开。解释普通用户能否使用、如何使用、成本多少、和上一代有什么已确认的差异。首次出现的技术术语用一句白话解释。不要写“根据某媒体/某公司博客/某新闻稿”。>

<!-- 如果已有文章或专题能帮助读者理解当前事实，在相关句子中加入 1–3 个上下文内链。锚文本应直接说明目标内容，不写“点击这里”“更多内容”。 -->

<!-- 仅当本节讨论 A 档数据图表时插入；优先使用清晰原图截图，不清晰时按 image-workflow.md 用 Image 2 根据已核验数据重制。 -->
![<指标名称 + 对比范围 + 图表类型>](<chart-url>)

## <用户怎么用>

<只写已经确认的开放范围、入口、步骤、价格或适用场景。没有确认的信息就不设对应小节，不用“尚不明确”“未公布”“没有官方口径”“缺少独立评测”“仍待实测”等句子占位。>

```

Frontmatter、blockquote 摘要和封面图 Markdown 行的生成逻辑保持不变。`<cover-url>` 必须来自 `examples/image-workflow.md` 生成并经用户确认上传的 Image 2 主题图；生成或上传失败时使用 `待补图`，不得改用网络图片或伪造 URL。`<chart-url>` 只在正文实际讨论 A 档数据图表时保留：按 `examples/image-workflow.md` 优先截取清晰原图，截图不清晰时再用 Image 2 根据已核验数据重制，上传前同样取得用户确认。正文段落使用 `article-writing` skill 根据 Stage 1 的 A 档已确认事实生成，不得改写模板区块，也不得补可靠信息之外的事实。

正文禁止出现信息源名称、来源列表或来源转述句式，例如“根据 X 新闻”“据 X 报道”“X 博客称”“官方公告显示”。不要在正文生成 `## 来源引用 (Sources)` 段；信源只用于内部校验和最终交付给用户，不写进文章主体。原图截图内已有的来源标记，以及 Image 2 重制图上的“根据 <来源> 数据重制”，属于图表完整性标记，不按正文来源列表删除。

正文也禁止把信息空缺当作内容，包括“目前尚不明确”“尚未披露”“未公布”“没有官方口径”“暂无官方信息”“缺少独立评测”“仍待实测”“待核实”“不能判断”“有待观察”及同义改写。遇到这类信息时，删除整条内容和对应小节。

## 开源表述规则

- 面向普通读者统一写“<项目或模型名> 开源”，不要写“开放权重”“开放模型权重”“公开权重”“权重开放”或类似行业表述。
- 英文信源使用 `open-weight`、`open weights`、`weights available` 等说法时，文章标题、摘要、正文和 SEO description 均转换为“开源”，不要直译或展开成“开放……权重”。
- 只改变措辞，不扩大事实范围。许可证、代码、训练数据或商用限制只有在得到 A 档事实支持且对读者有用时才单独说明；不要因为使用“开源”一词就自行补写这些内容。

示例：

- 不写：`某公司开放 Alpha 模型权重`
- 改写：`某公司开源 Alpha 模型`

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
description: 某公司发布 Alpha 模型，API 价格保持不变。本文梳理主要功能、可用渠道、定价变化，以及普通用户可以直接使用的入口。
sources:
  - name: 某公司 Alpha 模型官方公告
    url: https://example.com/alpha-model
    note: 发布日期、功能范围与使用入口
  - name: Alpha API 官方定价文档
    url: https://example.com/alpha-api-pricing
    note: API 价格
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
