# Tone Samples

Use these examples as calibration. The target voice is precise, easy to understand, and useful to a broad audience. The article should read like a technology explainer for everyday users, not a source-by-source news digest or an internal research memo.

## Launch News

Bad:

> 随着大模型技术的飞速发展，某公司再次带来震撼行业的 Alpha 模型，这一突破为 AI 应用打开了新的可能性。

Good:

> 某公司发布 Alpha 模型，并已开放 API。输入价格保持不变，开发者可以沿用现有接口接入。Alpha 模型支持文本和图片输入，普通用户可通过网页端直接体验。

## Funding News

Bad:

> 这笔融资无疑将进一步巩固公司的领先地位，也标志着 AI Agent 赛道进入新的发展阶段。

Good:

> 公司完成 2 亿美元 B 轮融资。本轮资金将用于扩充企业服务团队和推理基础设施，也就是承载模型运行的服务器与计算资源。

## Product Comparison

Bad:

> 相比上一代，新产品不仅性能更强，而且体验更好，展现出强大的市场潜力。

Good:

> 新版本把上下文窗口从 128K 提到 256K，价格不变。上下文窗口决定模型一次能处理多少内容；容量翻倍后，用户可以直接放入更长的文档或更多轮对话。

## PR Rewrite Signal

Bad:

> 多家媒体报道显示，该产品已经获得行业广泛认可。

Good:

> 产品已开放网页端和 API，个人用户可以直接注册使用。网页端适合日常问答和文档处理，API 面向需要把能力接入现有软件的开发者。

## Open-source Wording

Bad:

> 某公司开放 Alpha 模型权重，用户可以下载其开放权重版本。

Good:

> 某公司开源 Alpha 模型，用户可以下载使用。

这里的“开源”是面向普通读者的统一写法。若许可证、代码、训练数据或商用限制有 A 档事实支持且对读者有用，再另行准确说明；不要写“开放权重”“公开权重”“权重开放”或类似表达。

## 直述优先，避免装饰性比喻

能用准确、自然的字面表达讲清楚，就不要为了文采改成比喻、拟人或俏皮话。直接说明谁做了什么、发生了什么变化，以及对用户有什么影响。装饰性比喻会增加理解成本，也可能暗示原有事实并不支持的能力或效果。

以下改写仅演示表达方式，具体内容必须有已确认事实支持，不能把示例当作待写文章的事实。

| 刻意修饰 | 直接表达 |
| --- | --- |
| 这个参数是值得拨动的旋钮。 | 可以尝试调整这个参数。 |
| 显存问题依然绕不过去。 | 部署前仍需确认显存是否足够。 |
| 新版本为开发者铺平了接入道路。 | 开发者可以沿用现有接口。 |

为解释陌生概念而使用的类比可以保留，但必须准确、有助于理解，不能借类比暗示未经证实的能力或效果。不要把直述优先变成对所有比喻的机械禁用，也不要仅为追求字面表达而堆砌术语。

自检：**这句话具体是什么意思？直接写出那个意思。** 改写不得新增事实；没有具体信息可表达时，删掉空句。

## Editing Checklist

- Delete empty openers: `随着`, `近年来`, `在这个时代`.
- Delete broad conclusions: `未来可期`, `值得期待`, `打开新的可能性`.
- Replace adjectives with numbers when numbers exist.
- 用准确、自然的字面表达替换装饰性比喻、拟人或俏皮话；保留确实帮助理解且准确的类比。改写不得新增事实，没有具体信息的空句直接删除。
- Keep attribution in the research notes and handoff, not in the article body.
- Do not write `根据 X 新闻`, `据 X 报道`, `X 博客称`, `官方公告显示`, or source lists in the saved draft.
- Delete unconfirmed information instead of writing absence statements such as `目前尚不明确`, `尚未披露`, `未公布`, `没有官方口径`, `缺少独立评测`, `仍待实测`, `待核实`, `不能判断`, or synonyms.
- Assume a broad audience. Explain an unfamiliar term once in plain Chinese, then return to what users can do with the product or information.
- Replace `开放权重`, `开放模型权重`, `公开权重`, `权重开放`, and translations of `open-weight` with `<项目或模型名> 开源` in the title, summary, body, and SEO description.
- Do not end every section with `这意味着...`.
