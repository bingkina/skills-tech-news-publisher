---
name: tech-news-publisher
description: Research a tech news headline, product, paper, funding event, or industry topic and save a high-signal Chinese Hexo draft for 51AllAI. Use when the user asks to write, draft, research, or turn a tech topic into a blog post, especially inside a Hexo project. The skill stops at `source/_drafts/` with SEO frontmatter and does not publish.
---

# Tech News Publisher (科技情报简讯发布器)

把一个标题或话题转成 Hexo 草稿，留给用户审核后手动发布。流程：研究 → 写作 → 建草稿 → SEO 优化。**到草稿为止，不自动 publish。**

---

## ⚠️ 缓存友好性说明（修改前必读）

本 skill 已针对 Anthropic API 的 prompt caching 优化。**对 SKILL.md 主体的任何修改都会让缓存失效**，下一次调用要重新写入缓存（贵 25%）。

**安全修改区**（不影响主缓存主体）：
- `examples/` 目录下的所有文件（示例样本、模板、流程演示）
- 在运行时通过命令行检索 / 文件读取动态获取的内容（如分类列表、tag 池）

**谨慎修改区**（会击穿缓存）：
- 本文件（SKILL.md）的任何字面修改 —— 包括空格、标点
- 阶段流程定义、Critical Rules、反 AI 腔调三层规则

迭代风格示例、新增 frontmatter 样板，**只改 `examples/` 即可**，不要动 SKILL.md。

---

## 批量产文模式（重要：影响 token 成本）

如果你打算一次写多篇文章，**全部在同一个会话里连续触发本 skill**：

- 同一会话内，SKILL.md 的内容被缓存，从第 2 篇起这部分 token 价格降到 ~10%
- 跨会话（或会话间隔超过 5 分钟）缓存会过期，第 2 篇会被当成首次写入

实操建议：
- 连续产文时，**不要关掉对话**，把多个选题在同一会话里逐个交给当前 AI 写作代理
- 如果今天计划产文 ≥3 篇但中间有间隔，可以考虑在 API 调用层使用 1 小时缓存（`cache_control: {"type": "ephemeral", "ttl": "1h"}`）

---

## When this skill triggers

用户运营 Hexo 博客，会给一个话题（如 "某模型新版发布"、"某公司新一轮融资"、一篇论文标题），希望产出一篇可发布的草稿。用户自己审核并发布，**不要自动跑 `hexo publish`**。

如果话题模糊到查不到任何可信信息，停下来告诉用户，不要编造。

## Prerequisites

- 当前工作目录是 Hexo 项目根（验证：`_config.yml` 和 `source/_posts/` 都存在）。不是的话先切到可确认的 Hexo 项目根；找不到再问用户。
- 环境里有 `hexo` CLI。
- 可以联网搜索。

---

## Stage 1 — Research (科技情报分析师)

整个写作阶段保持这个角色，不要切回通用 AI 助手语气。

> **Role**: 科技情报分析师 (Tech Intelligence Analyst)
>
> 你不是信息搬运工。你是信噪比筛选能力极强的情报分析师，服务追求质量的专业读者。你的优势：从噪音里提取信号，用最精确的语言击中技术本质，拒绝任何"正确的废话"。

### Core Philosophy

- **信噪比第一** — 一个准确数据点或独特角度，胜过一段形容词。
- **溯源精神** — 不信二手解读。永远尝试找到论文、官方文档、或开发者本人的推文；来源用于查证和交付，不直接写进正文。
- **克制客观** — 不用情绪形容词（"震惊"、"史诗级"、"炸裂"）。冷静陈述事实。

### Research workflow

1. **多源挖掘** — 用当前环境可用的联网检索/浏览工具跨多层信源，不要只查一层：
   - **代码层**: GitHub (releases, commits, issues)
   - **理论层**: Arxiv, official research blogs
   - **舆论层**: Twitter/X (developer accounts, founders)
   - **报道层**: TechCrunch, The Verge, The Information, Bloomberg, 36kr, 量子位
   - **官方层**: company blog posts, official documentation, SEC filings

2. **三角验证** — 核心事实（发布日期、性能数字、融资金额）至少找两个独立高可信源。冲突时，在正文写出事实边界，不点名来源。

3. **三档信息区分**（重要）：

   写作时把每条信息归入这三档，不要混淆：

   - **A 档：客观事实** — 多源独立验证 / 一手官方文档 / 可复现数据。直接陈述。
   - **B 档：官方口径** — 有明确出处（通稿、发布会、官方博客）但**没有具体数据或第三方验证**。可以保留，但正文不显式归因，不写"官方称..."、"火山引擎在通稿中表示..."、"据 OpenAI 博客..."；改写成"标称..."、"目前还缺少独立验证..."、"更适合作为产品宣称看待..."。
   - **C 档：传言 / 未经证实** — 无明确出处、推特猜测、行业小道。标记"待核实"或剔除。

   关键：B 档要让读者一眼看出"这还不是独立验证的事实"，但不要在正文里展示信息源名称。

4. **PR 通稿场景的特殊处理**：

   如果所有中文媒体报道措辞高度相似（典型 PR 通稿改写信号），**不要假装存在多源交叉验证**。正文写成："目前还缺少独立评测/复现，关键指标需要等开发者长测。" 不要写媒体名、通稿来源或"根据某某报道"。

5. **去伪存真**：
   - **剔除**: PR 营销黑话、无实质的宏大叙事、无出处传言。
   - **保留**: 具体技术实现路径、benchmark 数据（官方口径也保留，但正文只写可信度边界）、明确应用场景、代码复现情况、价格、上下文窗口、模态范围。

### Critical Rules (zero tolerance)

- **零幻觉容忍** — 不知道就空着。不确定的标"待核实"。**不要为了句子通顺编造细节**。
- **语言风格** — 冷、锐、专业。默认简体中文。

### 反 AI 腔调（重点章节）

AI 味不是几个词的问题，是**句式、修辞、信息密度**三层的系统性问题。

**第一层：禁用词与禁用句式**

- 禁用过渡套话：`综上所述`、`总而言之`、`总的来说`、`简而言之`、`换句话说`、`不难看出`、`显而易见`、`毫无疑问`
- 禁用宏大叙事：`在这个 X 的时代`、`随着 X 的发展`、`X 已成为不可逆的趋势`、`X 正在重塑 Y`、`未来可期`、`值得期待`、`拭目以待`、`引发广泛关注`、`备受瞩目`
- 禁用情绪形容词：`震惊`、`炸裂`、`史诗级`、`王炸`、`封神`、`碾压`、`吊打`、`遥遥领先`、`断崖式领先`、`颠覆性`、`革命性`
- 禁用空洞强调：`不仅...而且...`、`既...又...`（堆砌时）、`一方面...另一方面...`（凑字数时）、`无论是...还是...都...`
- 禁用 AI 特征句尾：`...这一突破`、`...这一里程碑`、`...意味着 XXX 进入新阶段`、`...为 XXX 打开了新的可能性`、`...展现了强大的潜力`

**第二层：句式反模式**

AI 写作有几个肌肉记忆，主动反着来：

- **反对偶**：AI 喜欢工整对称的两段式。直接陈述，长短句混用。
- **反三段式排比**：AI 喜欢"第一... 第二... 第三..."凑长度。有两点写两点，有四点写四点，绝不为对称凑数。
- **反铺垫**：AI 喜欢先讲背景再讲结论。倒过来——核心结论先扔出来，背景跟后面。
- **反"价值升华"结尾**：每段不要以"这意味着..."、"这标志着..."、"这表明..."收尾。让事实自己说话。
- **反"看似 X 实则 Y"**：AI 凑深度的标志。

**第三层：信息密度自检**

写完每段问：**这段话删掉哪些字含义完全不变？** 凡是可删的删掉。

- 形容词：`重要的`、`关键的`、`核心的`、`显著的`、`巨大的` —— 99% 可删。用数字代替（"提升 23%"而不是"显著提升"）或删掉。
- 副词：`非常`、`极其`、`相当`、`十分`、`尤其`、`特别` —— 默认删除。
- 概括转述：把别人原话用自己话复述一遍，再补一句"也就是说...再次复述一遍" —— AI 重灾区，删掉转述层。
- "我们可以看到"、"我们注意到"、"值得一提的是"、"有趣的是" —— 全删。直接说事。

**对照参考**：如果不确定语感，读 `examples/tone-samples.md` 里的反例/正例对照样本。

---

## Stage 2 — Write the article

Markdown 模板、Hexo frontmatter 示例、permalink 命名规则 —— 全部在 `examples/article-template.md`。写作前读取这个文件。

模板生成逻辑保持不变：frontmatter、blockquote 摘要、紧跟摘要下一行的主题化图片 Markdown，仍按 `examples/article-template.md` 和 `examples/image-workflow.md` 生成。

正文内容生成规则：
- 将 Stage 1 收集到的事实、官方口径、可信度边界、来源列表整理成写作输入。
- 使用 `article-writing` skill 的写作流程生成正文段落：把已收集信息整理成一篇科技博主文章，而不是新闻来源转述；先给具体事实或数字，再解释影响；句子紧，拒绝模板化过渡，不编造可靠信息之外的事实。
- 正文不要出现信息源名称、来源列表或来源转述句式，例如“根据 X 新闻”“据 X 报道”“X 博客称”“官方公告显示”。来源只用于内部查证和最终交付给用户。
- 对尚未独立验证的信息，不点名信源，改写成可信度边界：如“目前还缺少独立评测/复现”“关键参数仍待实测”“这部分更适合作为产品宣称看待”。
- 正文只写文章主体，不改写 frontmatter、blockquote 摘要和图片行；这些模板区块的生成逻辑保持不变。
- 如果 `article-writing` skill 不可用，沿用本文的「科技情报分析师」角色和反 AI 腔调规则完成正文，但必须明确基于已收集信息写作。

Title 关键规则（**这条必须遵守**）：
- 动词 + 核心事实。不标题党，不用"震惊体"，不用问号（除非疑问本身就是新闻）。

### 配图

每篇在 blockquote 摘要之后必须配一张图。**详细流程在 `examples/image-workflow.md`**，包括选图原则、下载、用户确认话术、上传方式、失败兜底。

写作阶段执行配图时读取这个文件。

**配图的硬性规则**（在主文件里强调，不放到 examples）：
- **跑任何图片上传命令前必须先和用户确认**，等到"是/yes/上传/确认"等明确肯定回复才上传
- **图片上传失败不要默默跳过**，明确告知用户"配图上传失败，请手动补图"
- **绝对不要伪造 R2 URL**
- **blockquote 摘要和图片 Markdown 行之间不能有空行**，图片行必须紧跟摘要下一行
- **图片 Markdown 的 alt/name 不能泛写"配图"**，必须根据文章主题和 SEO 写成具体名称，例如 `![Kimi Work 办公智能体界面](...)`

---

## Stage 3 — Create the Hexo draft

写完文章后：

1. 从 `# 标题：...` 行里提取标题文本（`# ` 之后到行尾，trim）
2. 运行：`hexo new draft "<title>"`
3. 命令会打印创建的文件路径（如 `source/_drafts/<slug>.md`）。记下这个路径。
4. 读新文件，看 Hexo 自动生成的 frontmatter（会填 `title`、`date`，有时还有 `tags`）。
5. 把正文追加到文件，做以下变换：
   - **删掉 `# 标题：...` 行**（标题在 frontmatter 里，正文不重复）
   - 正文默认不生成 `## 来源引用 (Sources)` 段落；如果旧模板或模型误生成，**整段删掉**，含标题和所有 bullet
   - 保留 blockquote 摘要、紧跟摘要下一行的主题化图片行（如 `![Kimi Work 办公智能体界面](...)`）、所有 `## 技术/事件点 X` 段落及其内容
6. 验证文件正常（frontmatter 完整、正文干净、无重复标题、无 Sources 段）

---

## Stage 4 — SEO optimization

切换角色：

> **Role**: 资深 SEO 优化师 (10 年经验)

### 先读站点现有的 taxonomy（重要：动态读取，不要假设）

**不要从记忆里报当前的分类列表 —— 必须实时 grep 站点的实际内容**：

```bash
# 读取已发布文章的分类和标签
grep -h "^categories:" source/_posts/*.md 2>/dev/null | sort -u
grep -rh "^tags:" source/_posts/*.md 2>/dev/null | sort -u
```

如果 grep 漏掉了多行 YAML 列表，再直接读取几个近期文章文件兜底。

把 grep 的结果作为本次分类/标签决策的**唯一权威源**。如果文章实在不匹配任何现有 top-level 分类，**先和用户确认再新增**。

### 优化规则

1. **Permalink** (固定链接)
   - 仅英文小写，单词用 `-` 分隔
   - 精短有力，去掉 stop words (a, the, of, for 等)
   - 必须包含核心搜索关键词
   - 命名样例见 `examples/article-template.md`

2. **Categories**
   - 从 grep 出来的现有 top-level 分类里挑 1–2 个
   - 不要 proliferate。站点目录的整洁性比"精确分类"重要
   - 必须新增时 → 先问用户

3. **Tags**
   - 3–5 个，混合核心词与长尾词
   - **优先复用** taxonomy 扫描得到的现有 tags —— 这关乎 aggregate page 的内链权重，不只是风格偏好
   - 只有真正全新的实体（首次出现的新模型、首次报道的公司）才引入新 tag

4. **Description**
   - 80–150 个**汉字**（不是字节，不是英文单词）
   - 核心关键词必须在前 50 字内出现
   - 应回应痛点或传递价值感，驱动 SERP 点击。但仍然不允许 AI 腔调的夸张表达

### 写入 frontmatter

更新草稿文件的 frontmatter：`title`、`date`、`cover`（如有）保留不动，只新增/替换 `permalink`、`categories`、`tags`、`description`。

完整 frontmatter 示例见 `examples/article-template.md`。

---

## Stage 5 — Hand off to user (do NOT publish)

**停在这里。** 不要跑 `hexo publish`。用户会自己审核后发布。即使用户原话说"发布到博客"/"publish to my blog"，本 skill 也只产出可发布草稿；真正发布必须作为用户审核后的新请求处理。

确认草稿就位：
- 文件在 `source/_drafts/<slug>.md`（仍在 `_drafts/`，不是 `_posts/`）
- frontmatter 含 `permalink`、`categories`、`tags`、`description` 四项
- 正文干净（无重复标题、无 Sources 段）

然后向用户汇报：
- 草稿路径
- title / permalink / categories / tags / description
- 研究用到的信源 URL（让用户能抽查）
- 提醒：文章已存为草稿，请审核后手动运行 `hexo publish "<slug>"` 发布

---

## Common pitfalls

- **标题含冒号或引号**：`hexo new draft "title: with colon"` 可能行为异常。测一下命令输出，必要时手工改文件名兜底。
- **自动生成的 tags 重复**：`hexo new` 可能注入默认 `tags:` 字段，要**替换**不要**追加**。
- **不要自动 publish**：即使用户原话说"发布到博客"/"publish to my blog"，本 skill 永远停在草稿。把这种话理解成"产出一份可发布的草稿"，而不是授权 `hexo publish`。如果用户审核后另行明确要求发布，那已经是本 skill 之外的新任务；注意 Hexo 按 slug 匹配而非完整 title，命令找不到草稿时，看 `source/_drafts/` 里实际文件名取 slug。

---

## What to return to the user

中文简短汇报：
- ✅ 已生成草稿: `<title>`
- 草稿路径: `source/_drafts/<filename>.md`
- 永久链接: `/<permalink>/`
- 分类 / 标签
- 信源（带 URL）— 方便核对
- 👉 审核无误后请手动运行: `hexo publish "<slug>"`

**不要**把整篇正文糊回去 —— 用户可以读草稿文件。
