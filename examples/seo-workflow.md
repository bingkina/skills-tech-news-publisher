# SEO Workflow for 51AllAI Drafts

Read this file before research and again before final validation. It controls page-level SEO for a single draft; site-wide templates, robots rules, sitemaps, schema infrastructure, publishing, and Search Console submission remain outside this draft workflow.

## 1. Build an internal SEO Brief

Search published posts and drafts before choosing the angle. Use `rg` so an empty result does not fail because of shell glob expansion.

```bash
rg -n -i "<entity>|<product>|<event keyword>" source/_posts source/_drafts
rg -n "^(title|permalink|tags|categories):" source/_posts source/_drafts
```

Record this internal brief:

```yaml
primary_entity: <official entity or product name>
event_type: <release|funding|paper|policy|product update>
primary_intent: <the main question a searcher needs answered>
secondary_intents:
  - <availability, price, comparison, usage, limits, or another supported need>
existing_related_posts:
  - <existing permalink and why it is relevant>
topic_hub: <existing topic page, if relevant>
distinct_angle: <new value supported by A-grade facts>
candidate_title: <entity + action + differentiating fact>
candidate_slug: <short English slug>
```

Treat an article as a likely duplicate when it covers the same entity, event, and user intent, even if its wording differs. A new article needs a distinct factual purpose, such as a new release channel, material price change, independently verified benchmark, implementation guide, or clearly different audience. Do not manufacture an angle from B/C-grade claims.

## 2. Map evidence to user questions

For each intended section, list the user question, the answer, and its A-grade source. Remove a section when its answer cannot be supported. Favor concrete facts that help a reader decide or act:

- what changed and when;
- who can use it and in which regions or plans;
- exact entry point or setup path;
- price and a useful calculation from verified rates;
- differences from the previous version or a closely related product;
- confirmed limits that materially affect use.

The article should add editorial value beyond restating an announcement. Valid value includes a calculation using published prices, a compact comparison using verified specifications, or a plain-language explanation connecting a technical constraint to the user's choice. Label company-reported benchmarks accurately and do not turn them into independent conclusions.

## 3. Write for extraction and reading

- Put the direct answer in the blockquote summary: entity, action, date or availability, and the most useful confirmed change.
- Use H2 headings that answer real questions or state concrete facts. Do not mechanically create FAQ headings.
- Keep important facts in HTML text. Do not leave essential numbers only inside a cover or chart.
- Introduce the official English name and common Chinese name naturally when both help entity recognition; do not repeat variants as keywords.
- Use a table only when it makes several comparable facts easier to scan.

## 4. Add contextual internal links

Add one to three links only when an existing article or topic page helps the reader understand the current paragraph. Link from descriptive text such as `Hy4 preview 的模型参数与 API 价格`, not `点击这里` or `更多内容`.

Prefer, in order:

1. the closest prior article needed for context;
2. a comparison or predecessor article;
3. an existing topic hub.

The site's automatic related-post block supplements these links but does not replace them. Verify every local target exists. Do not force links merely to reach a quota.

## 5. Prepare metadata

### Title

Use the official entity name, an action, and the most differentiating confirmed fact. Keep it concise and unique among existing titles. Avoid repeating the same keyword, boilerplate, unsupported superlatives, or a vague title that omits the entity.

### Permalink

Use `posts/YYYY/MM/<slug>/`. Keep the slug lowercase, descriptive, stable, and usually three to seven English words. Include the entity; do not encode disposable marketing wording.

### Categories and tags

Read current taxonomy every time. Choose one or two existing categories. Use two to five stable entity/product/topic tags and reuse existing spelling. Because related posts use exact shared tags, avoid one-off long-tail query phrases.

### Description

Write one or two accurate, unique sentences. Put the entity and event near the beginning, then state the concrete information the page provides. A practical editorial target is 70–120 Chinese characters, but accuracy and usefulness take precedence over length.

### Sources

Write every source used by the final article as structured frontmatter:

```yaml
sources:
  - name: <clear source title>
    url: <canonical HTTP(S) URL without credentials or tracking parameters>
    note: <short description of the facts verified>
```

Prefer canonical official pages. A source list in chat or prose is not a substitute for frontmatter. Do not create a Markdown Sources section in the body.

## 6. Validate the built draft

Run the repository's existing checks without installing new dependencies:

```bash
node --test test/*.test.mjs
npx hexo generate --draft
git diff --check
```

If the repository does not contain `test/*.test.mjs`, skip only that command and report it. Resolve the draft permalink to `public/<permalink>/index.html`, then verify:

- one descriptive title and one visible H1 represent the same article;
- meta description is present and matches the final facts;
- canonical URL equals the intended permalink;
- Open Graph title, description, URL, and image are present;
- image alt text describes the subject;
- `NewsArticle` JSON-LD parses and matches the visible title, dates, author/publisher, image, category, tags, and sources;
- `dateModified` is not fabricated by an unnecessary `updated` field;
- visible “原始来源” and JSON-LD citation contain the structured `sources`;
- internal links resolve to existing local pages;
- no duplicate title, duplicate permalink, information-gap sentence, or body Sources section remains.

Draft URLs do not need to appear in the production sitemap before publication. Sitemap, news sitemap, live HTTP status, indexing, and Search Console checks belong to a separate post-publication request.

## Avoid generic SEO additions

- Do not add `meta keywords`.
- Do not add FAQ content or `FAQPage` Schema unless the page truly needs a visible reader-facing Q&A and the site owner separately chooses to support it.
- Do not add schema directly inside an article when the theme already emits `NewsArticle`, organization, website, and breadcrumb data.
- Do not invent statistics, quotations, or repeated keyword variants for GEO.
- Do not treat experimental GEO percentage lifts as guaranteed platform results.
