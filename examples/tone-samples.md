# Tone Samples

Use these examples as calibration. The target voice is precise, blog-like, and evidence-aware. The article should read like a tech blogger's analysis, not a source-by-source news digest.

## Launch News

Bad:

> 随着大模型技术的飞速发展，某公司再次带来震撼行业的 Alpha 模型，这一突破为 AI 应用打开了新的可能性。

Good:

> 某公司发布 Alpha 模型。推理延迟标称下降 18%，API 输入价格不变。第三方 benchmark 还没有稳定复现，现阶段不能把性能提升当成实测结论。

## Funding News

Bad:

> 这笔融资无疑将进一步巩固公司的领先地位，也标志着 AI Agent 赛道进入新的发展阶段。

Good:

> 公司完成 2 亿美元 B 轮融资，投后估值未披露。这笔钱主要会流向企业销售和推理基础设施。收入、留存率和客户续约数据都没有公开，所以还不能判断它是不是已经跑通商业化。

## Product Comparison

Bad:

> 相比上一代，新产品不仅性能更强，而且体验更好，展现出强大的市场潜力。

Good:

> 新版本把上下文窗口从 128K 提到 256K，价格不变。长上下文召回率还缺少公开实测，实际收益取决于检索和引用稳定性。

## PR Rewrite Signal

Bad:

> 多家媒体报道显示，该产品已经获得行业广泛认可。

Good:

> 目前能看到的发布说法高度一致，独立评测、GitHub issue 复现记录和开发者长测都还缺位。这类产品先看 demo 很容易兴奋，真正的判断点在连续使用一周后的稳定性。

## Editing Checklist

- Delete empty openers: `随着`, `近年来`, `在这个时代`.
- Delete broad conclusions: `未来可期`, `值得期待`, `打开新的可能性`.
- Replace adjectives with numbers when numbers exist.
- Keep attribution in the research notes and handoff, not in the article body.
- Do not write `根据 X 新闻`, `据 X 报道`, `X 博客称`, `官方公告显示`, or source lists in the saved draft.
- Do not use `口径` in article body; prefer `产品宣称`, `发布说法`, or `现有信息`.
- Do not end every section with `这意味着...`.
