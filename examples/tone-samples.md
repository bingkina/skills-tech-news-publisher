# Tone Samples

Use these examples as calibration. The target voice is cold, precise, and source-aware.

## Launch News

Bad:

> 随着大模型技术的飞速发展，某公司再次带来震撼行业的 Alpha 模型，这一突破为 AI 应用打开了新的可能性。

Good:

> 某公司发布 Alpha 模型。官方称推理延迟下降 18%，API 输入价格不变。第三方 benchmark 还没有稳定复现，现阶段只能把性能提升视为官方口径。

## Funding News

Bad:

> 这笔融资无疑将进一步巩固公司的领先地位，也标志着 AI Agent 赛道进入新的发展阶段。

Good:

> 公司完成 2 亿美元 B 轮融资。领投方是 X，投后估值未披露。融资用途集中在企业销售和推理基础设施，没有公布收入、留存率或客户续约数据。

## Product Comparison

Bad:

> 相比上一代，新产品不仅性能更强，而且体验更好，展现出强大的市场潜力。

Good:

> 新版本把上下文窗口从 128K 提到 256K，价格不变。官方没有公布长上下文召回率测试，实际收益取决于检索和引用稳定性。

## PR Rewrite Signal

Bad:

> 多家媒体报道显示，该产品已经获得行业广泛认可。

Good:

> 目前中文报道措辞高度相似，基本转引官方通稿。没有看到独立评测、GitHub issue 复现记录或开发者长测。

## Editing Checklist

- Delete empty openers: `随着`, `近年来`, `在这个时代`.
- Delete broad conclusions: `未来可期`, `值得期待`, `打开新的可能性`.
- Replace adjectives with numbers when numbers exist.
- Keep attribution visible when the fact only comes from a company blog or press release.
- Do not end every section with `这意味着...`.
