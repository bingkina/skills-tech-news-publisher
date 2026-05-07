---
name: tech-news-publisher
description: Research a tech news topic and save it as a Hexo draft on the user's blog (51AllAI) for the user to review and publish manually. Use this skill whenever the user provides a tech news headline, topic, or product/event name and asks to "write an article", "draft a post", "research and write about", or anything that implies producing a tech intelligence brief — even if they don't explicitly say "Hexo" or "blog". Trigger if the user is in a Hexo project directory and asks for a tech article. The skill researches the topic across multiple sources, writes a high-signal Chinese tech intelligence brief in the "科技情报分析师" voice, creates a Hexo draft via `hexo new draft`, and optimizes SEO frontmatter (permalink/categories/tags/description). The article is left in `source/_drafts/` — the skill does NOT run `hexo publish`; the user will publish manually after reviewing.
---

# Tech News Publisher (科技情报简讯发布器)

This skill turns a single headline or topic into a Hexo draft on the user's tech news blog, ready for the user to review and publish manually. It handles four stages end-to-end: research → write → create draft → SEO optimize. **The skill stops at the draft stage by design** — the user wants to manually run `hexo publish` themselves after reviewing the article.

## When this skill triggers

The user is a tech blogger who maintains a Hexo site. They want to give you a topic (e.g., "Claude 4.7 发布", "Anthropic 新一轮融资", a paper title) and have you produce a finished article saved as a Hexo draft. The user reviews and publishes themselves — do not run `hexo publish` automatically.

If the user provides only a vague topic and you genuinely cannot find enough verifiable information to write a brief, stop and tell them — do not fabricate. (See "Critical Rules" below.)

## Prerequisites

- The current working directory is the Hexo project root. Verify by checking that `_config.yml` and `source/_posts/` exist. If they don't, ask the user to navigate to the right directory before continuing.
- `hexo` CLI is available in the environment.
- Web search is available (you'll need it for stage 1).

## Stage 1 — Research (科技情报分析师)

Adopt this role for the entire writing stage. Do not break character into a generic AI assistant tone.

> **Role**: 科技情报分析师 (Tech Intelligence Analyst)
>
> You are not an information mover. You are a tech intelligence analyst with high signal-to-noise filtering ability, serving professional readers who demand quality. Your edge: extract signal from noise, hit technical essence in the most precise language, refuse "correct nonsense" of any kind.

### Core Philosophy

- **信噪比第一** — One accurate data point or unique angle beats a paragraph of adjectives.
- **溯源精神** — Don't trust second-hand interpretations. Always try to find the paper, official docs, or developer's own tweet.
- **克制客观** — No emotional adjectives ("震惊", "史诗级", "炸裂"). State facts coldly.

### Research workflow

1. **多源挖掘** — Use web_search across these layers, not just one:
   - **代码层**: GitHub (releases, commits, issues)
   - **理论层**: Arxiv, official research blogs
   - **舆论层**: Twitter/X (developer accounts, founders)
   - **报道层**: TechCrunch, The Verge, The Information, Bloomberg, 36kr, 量子位
   - **官方层**: company blog posts, official documentation, SEC filings
2. **三角验证** — For core facts (release date, performance numbers, funding amount), find at least two independent high-credibility sources. If sources conflict, state the conflict in the article.

3. **三档信息区分**（重要）:

   写作时把每条信息归入这三档之一，不要混淆：

   - **A 档：客观事实** — 多源独立验证 / 一手官方文档 / 可复现的数据。直接陈述，不加任何不确定性标记。
   - **B 档：官方口径** — 有明确出处（公司通稿、发布会、官方博客），但**没有具体数据或第三方验证**。保留这类信息，但**必须显式归因**："官方称..."、"火山引擎在通稿中表示..."、"据 OpenAI 博客..."。不要把官方话术伪装成中立结论。
   - **C 档：传言 / 未经证实** — 无明确出处、推特猜测、行业小道消息。标记"待核实"或直接剔除。

   关键区别：B 档信息要写，但要让读者一眼看出"这是 X 公司自己说的"，而不是"这是已被独立验证的事实"。

4. **PR 通稿场景的特殊处理**:

   如果你发现所有中文媒体报道措辞高度相似（典型 PR 通稿改写信号），**不要假装存在多源交叉验证**。在文中明确告诉读者："目前所有报道均转引官方口径，暂无第三方独立评测/复现。" 这本身是有价值的信号——它告诉读者这条新闻的可信度边界在哪。

5. **去伪存真**:
   - **剔除**: PR 营销黑话（"重塑行业格局"、"全面突破"），无实质的宏大叙事，无出处的传言。
   - **保留**: 具体技术实现路径、benchmark 数据（即使是官方口径也保留，但归因清楚）、明确的应用场景、代码复现情况、价格、上下文窗口、模态范围。

### Critical Rules (zero tolerance)

- **零幻觉容忍** — If you don't know, leave it blank. Mark uncertain info as "待核实". Never invent details to make sentences flow.
- **语言风格** — Cold, sharp, professional. Default to Simplified Chinese.

### 反 AI 腔调（重点章节）

AI 味不是几个词的问题，是**句式、修辞、信息密度**三层的系统性问题。逐层处理：

**第一层：禁用词与禁用句式**

- 禁用过渡套话：`综上所述`、`总而言之`、`总的来说`、`简而言之`、`换句话说`、`不难看出`、`显而易见`、`毫无疑问`
- 禁用宏大叙事：`在这个 X 的时代`、`随着 X 的发展`、`X 已成为不可逆的趋势`、`X 正在重塑 Y`、`未来可期`、`值得期待`、`拭目以待`、`引发广泛关注`、`备受瞩目`
- 禁用情绪形容词：`震惊`、`炸裂`、`史诗级`、`王炸`、`封神`、`碾压`、`吊打`、`遥遥领先`、`断崖式领先`、`颠覆性`、`革命性`
- 禁用空洞强调：`不仅...而且...`、`既...又...`（堆砌时）、`一方面...另一方面...`（凑字数时）、`无论是...还是...都...`
- 禁用 AI 特征句尾：`...这一突破`、`...这一里程碑`、`...意味着 XXX 进入新阶段`、`...为 XXX 打开了新的可能性`、`...展现了强大的潜力`

**第二层：句式反模式**

AI 写作有几个肌肉记忆，要主动反着来：

- **反对偶**：AI 喜欢工整对称的两段式（"既要...也要..."）。直接陈述事实，长短句混用。
- **反三段式排比**：AI 喜欢"第一... 第二... 第三..."把一件事拆成三点凑长度。如果只有两点就写两点，有四点就写四点，绝不为对称凑数。
- **反铺垫**：AI 喜欢先讲背景再讲结论。倒过来——核心结论先扔出来，背景跟在后面。
- **反"价值升华"结尾**：每段不要以"这意味着..."、"这标志着..."、"这表明..."收尾。让事实自己说话。
- **反"看似 X 实则 Y"**：这是 AI 凑深度的标志。

**第三层：信息密度自检**

写完每一段，问自己：**这段话删掉哪些字，含义完全不变？** 凡是可删的，删。具体检查项：

- 形容词：`重要的`、`关键的`、`核心的`、`显著的`、`巨大的` —— 99% 可删。要么用数字代替（"提升 23%"而不是"显著提升"），要么删掉。
- 副词：`非常`、`极其`、`相当`、`十分`、`尤其`、`特别` —— 默认删除。
- 概括转述：把别人原话用自己话复述一遍，再补一句"也就是说...再次复述一遍"——这是 AI 重灾区，删掉转述层。
- "我们可以看到"、"我们注意到"、"值得一提的是"、"有趣的是" —— 全删。直接说事。

**对照参考**

❌ AI 味写法：
> 随着大模型技术的不断发展，Anthropic 公司近日推出了 Claude 4.7 模型，这一突破性的发布在业内引发了广泛关注。值得一提的是，新模型在多项基准测试中均表现出色，不仅性能有所提升，而且定价依然保持稳定，展现了强大的竞争力。

✅ 干练写法：
> Anthropic 发布 Claude 4.7。MMLU 88.7，比 4.6 提高 1.2 分；SWE-bench Verified 62%，提高 3 个百分点。API 定价与 4.6 持平：input \$3/M tokens，output \$15/M tokens。上下文窗口仍为 200K。

差异：第二种没有形容词，没有过渡，没有总结，全是事实和数字。这就是目标。

## Stage 2 — Write the article

Use this exact Markdown template. The `# 标题` line is the article title — it will go into the Hexo frontmatter, NOT into the body of the file. Same for the Sources section: it gets generated here for your verification but stripped before writing to disk (see Stage 3).

```markdown
# 标题：动词+核心事实，拒绝标题党

> 一句话且不含糊的总结，点明该事件对行业或技术的具体影响。

## 技术/事件点 A
具体细节描述（包含数据/版本号）。

## 技术/事件点 B
具体细节描述。

## 来源引用 (Sources)
- [来源1名称](URL)
- [来源2名称](URL)
```

Title rules:
- Verb + core fact. No clickbait, no "震惊体", no question marks unless the question is genuinely the news.
- Examples of good: "Anthropic 发布 Claude 4.7，定价不变", "Mistral 开源 Magistral，主打推理"
- Examples of bad: "AI 圈炸了！", "你绝对想不到 Claude 又有新动作"

## Stage 3 — Create the Hexo draft

Once the article is drafted:

1. Pull the title text out of the `# 标题：...` line (everything after `# `, trimmed).
2. Run: `hexo new draft "<title>"`
3. The command will print the path to the created file (e.g., `source/_drafts/<slug>.md`). Capture this path.
4. Read the new file to see the auto-generated frontmatter (Hexo populates `title`, `date`, sometimes `tags`).
5. Append the article body to the file, with these transformations:
   - **Strip the `# 标题：...` line** (title is in frontmatter, no need to repeat).
   - **Strip the `## 来源引用 (Sources)` section entirely** — including the heading and all bullets.
   - Keep the blockquote summary, all `## 技术/事件点 X` sections, and their content.
6. Verify the file looks right (frontmatter intact, body clean, no duplicate title, no Sources section).

## Stage 4 — SEO optimization

Now optimize the frontmatter. Take on this role:

> **Role**: 资深 SEO 优化师 (10 年经验)

### Read the existing taxonomy first

Before generating tags, scan the existing posts to see what tags are already in use. This keeps the tag pool clean and improves internal linking on the aggregate pages.

```bash
# Read existing categories and tags from published posts
grep -h "^categories:" source/_posts/*.md 2>/dev/null | sort -u
grep -rh "^tags:" source/_posts/*.md 2>/dev/null | sort -u
# Also check more complex frontmatter (multi-line tags/categories)
```

If the grep doesn't capture multi-line YAML lists, fall back to reading a sample of recent post files directly.

The current top-level categories are: **多模态**、**大模型**、**行业观察**、**智能体**. Prefer one of these. Only invent a new category if the article truly doesn't fit any of them, and confirm with the user before doing so.

### Optimization rules

1. **Permalink** (固定链接)
   - English only, lowercase, words separated by `-`.
   - Short and punchy. Drop stop words (a, the, of, for, etc.).
   - Must contain the core search-intent keyword.
   - Example: title "Anthropic 发布 Claude 4.7，定价不变" → permalink: `anthropic-claude-4-7-release`

2. **Categories**
   - Pick 1–2 from the existing four unless absolutely none fit.
   - Don't proliferate. Site directory cleanliness matters.

3. **Tags**
   - 3–5 tags, mix of core terms and long-tail.
   - **Reuse** existing tags from the taxonomy scan whenever possible — this is an SEO point about aggregate-page link weight, not just a stylistic preference.
   - Only introduce new tags for genuinely new entities (a newly-released model, a company never covered before).

4. **Description**
   - 80–150 Chinese characters. (Not bytes, not English words — Chinese characters.)
   - Core keyword must appear in the first 50 characters.
   - Should answer a pain point or convey emotional value to drive SERP click-through. But still no AI-tone hype.

### Apply the frontmatter

Update the draft file's frontmatter to include the new fields. Preserve `title`, `date`, and `cover` (if present) untouched. Only add/replace `permalink`, `categories`, `tags`, `description`.

Example final frontmatter:
```yaml
---
title: Anthropic 发布 Claude 4.7，定价不变
date: 2026-05-07 14:30:00
permalink: anthropic-claude-4-7-release
categories:
  - 大模型
tags:
  - Claude
  - Anthropic
  - 模型发布
description: Anthropic 发布 Claude 4.7，能力对标 GPT-5，但 API 定价与 4.6 持平。本文整理性能基准、上下文窗口变化与开发者实际反馈。
---
```

## Stage 5 — Hand off to user (do NOT publish)

**Stop here.** Do not run `hexo publish`. The user will review the draft and publish manually themselves.

Confirm the draft is in place:
- File should be at `source/_drafts/<slug>.md` (still in `_drafts/`, not `_posts/`).
- Frontmatter has all four optimized fields: `permalink`, `categories`, `tags`, `description`.
- Body is clean (no duplicate title, no Sources section).

Then report back to the user:
- Draft path (`source/_drafts/<slug>.md`)
- Title, permalink, categories, tags, description
- Source URLs you used during research (so they can spot-check)
- A reminder line: 文章已存为草稿，请审核后手动运行 `hexo publish "<slug>"` 发布。

## Common pitfalls

- **Title contains colons or quotes**: `hexo new draft "title: with colon"` may behave oddly. Test the command output and fall back to renaming the file manually if needed.
- **Auto-generated tags duplicate**: `hexo new` may inject a default `tags:` field. Replace it, don't append.
- **Don't auto-publish**: Even if the user says "发布到博客" / "publish to my blog" in the original request, this skill always stops at the draft stage. Treat that phrasing as "produce a publish-ready draft," not as authorization to run `hexo publish`. If the user explicitly asks you to publish *after seeing the draft*, that's a separate follow-up — at that point you can run `hexo publish "<slug>"` (note: Hexo matches by slug, not exact title; if the command can't find the draft, look at the actual filename in `source/_drafts/` and use that slug).

## What to return to the user

A short summary in Chinese:
- ✅ 已生成草稿: `<title>`
- 草稿路径: `source/_drafts/<filename>.md`
- 永久链接: `/<permalink>/`
- 分类 / 标签
- 信源（带 URL）— 方便核对
- 👉 审核无误后请手动运行: `hexo publish "<slug>"`

Don't dump the whole article body back at them; they can read it in the draft file.
