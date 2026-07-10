# GEO 优化规范指南

> Generative Engine Optimization — 让 AI 引擎更好地理解、检索和引用你的内容。

## 1. 答案优先结构 (Answer-First)

AI 引擎在检索时优先提取首段内容作为答案来源。

**要求：**
- 第一段必须包含对该主题的直接回答（50-150 字）
- 使用 `## 核心要点` 或 `## 摘要` 小节提炼关键信息
- 避免铺垫式开头，直接给出结论

**示例：**

```markdown
# 什么是 GEO？

GEO（Generative Engine Optimization，生成引擎优化）是一种内容优化方法，
旨在让 AI 生成引擎（如 ChatGPT、Gemini、Perplexity）能够更准确地检索、
理解并引用你的内容。与 SEO 面向人类搜索不同，GEO 面向 AI 引擎的理解逻辑。

## 核心要点

- GEO 优化 AI 引擎的内容检索与引用效率
- 核心方法包括结构化数据、答案优先、实体关系标注
- 适用于产品文档、技术文档、营销内容等
```

## 2. 结构化数据 (JSON-LD Schema)

为每个知识条目提供 JSON-LD 结构化数据，帮助 AI 引擎识别实体类型和关系。

**必须包含的 Schema 类型：**

| 内容类型 | Schema Type | 文件位置 |
|---------|-------------|---------|
| 文章 | `Article` / `TechArticle` | `schema/{slug}.jsonld` |
| FAQ | `FAQPage` | `docs/faq-schema.json` |
| 产品 | `Product` | `schema/product-{name}.jsonld` |
| 组织 | `Organization` | `schema/organization.jsonld` |
| 定义/术语 | `DefinedTerm` | `schema/term-{name}.jsonld` |

**JSON-LD 模板：**

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "文章标题",
  "description": "一句话摘要",
  "author": {
    "@type": "Organization",
    "name": "组织名称"
  },
  "datePublished": "2026-07-10",
  "dateModified": "2026-07-10",
  "keywords": ["关键词1", "关键词2"],
  "about": [
    {
      "@type": "DefinedTerm",
      "name": "核心实体名",
      "description": "实体定义"
    }
  ]
}
```

## 3. 实体关系标注

明确标注内容中的实体及其关系，帮助 AI 构建知识图谱。

**规则：**
- 首次出现的专有名词用 **粗体** 标注
- 使用 `## 相关概念` 小节列出关联实体
- 在 `schema/knowledge-graph.jsonld` 中维护实体关系图

**实体关系类型：**
- `isA` — 分类关系（A 是 B 的一种）
- `partOf` — 组成关系（A 是 B 的一部分）
- `relatedTo` — 关联关系（A 与 B 相关）
- `enables` — 使能关系（A 使 B 成为可能）
- `conflictsWith` — 冲突关系（A 与 B 互斥）

## 4. FAQ 自然语言匹配

覆盖用户可能用自然语言提出的问题和变体。

**要求：**
- 每个主题至少覆盖 3-5 个 FAQ
- 问题使用自然语言（口语化），不用技术术语提问
- 答案保持简洁，首句直接回答
- 使用 `## 常见问题` 小节

**FAQ JSON-LD 格式：**

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "用户会怎么问这个问题？",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "直接、简洁的答案，50字以内。"
      }
    }
  ]
}
```

## 5. 权威引用与来源

AI 引擎倾向于引用有明确来源的内容。

**规则：**
- 数据、统计、结论必须标注来源
- 使用 `[来源名](URL)` 格式引用
- 在文末 `## 参考文献` 小节列出完整引用
- 优先引用权威来源（学术论文、官方文档、行业报告）

## 6. 语义清晰性

避免歧义，确保 AI 引擎能准确理解内容含义。

**规则：**
- 避免代词指代不清（用具体名词代替"它"、"这个"）
- 首次出现缩写时给出全称（如 "GEO（Generative Engine Optimization）"）
- 使用主动语态，避免被动语态
- 列表使用有序/无序列表，不用段落堆砌
- 代码/命令用代码块标注语言类型

## 7. 内容深度与广度

AI 引擎偏好全面、有深度的内容。

**要求：**
- 每个主题覆盖：定义、原理、方法、示例、最佳实践、常见误区
- 文章长度建议 800-2000 字（核心主题可更长）
- 提供具体示例和代码/配置片段
- 包含对比分析（如方案 A vs 方案 B）

## 8. 元数据规范

每篇文章头部必须包含 YAML front matter：

```yaml
---
title: "文章标题"
slug: "url-friendly-slug"
description: "一句话描述，150字以内"
date: 2026-07-10
updated: 2026-07-10
tags: ["标签1", "标签2"]
category: "分类"
entities: ["实体1", "实体2"]
priority: high | medium | low
---
```

## 9. 内部链接策略

建立知识条目间的内部链接，形成知识网络。

**规则：**
- 每篇文章至少链接 3-5 篇相关文章
- 使用描述性锚文本（不用"点击这里"）
- 在 `## 延伸阅读` 小节列出推荐阅读顺序
- 维护 `sitemap.md` 中的链接关系图

## 10. 持续维护

- 定期审查内容准确性和时效性
- 根据 AI 引擎的引用反馈调整内容结构
- 新增主题时同步更新知识图谱和 FAQ
- 每季度更新一次 `dateModified`

---
*本规范随 GEO 实践持续演进*
