---
title: "JSON-LD 结构化数据指南"
slug: "jsonld-guide"
description: "JSON-LD 是 GEO 优化的核心技术，通过在内容中嵌入 Schema.org 结构化数据，帮助 AI 引擎理解实体类型和关系。"
date: 2026-07-10
updated: 2026-07-10
tags: ["JSON-LD", "Schema.org", "结构化数据", "GEO"]
category: "技术实现"
entities: ["JSON-LD", "Schema.org", "结构化数据", "实体"]
priority: high
---

# JSON-LD 结构化数据指南

**JSON-LD（JavaScript Object Notation for Linked Data）** 是一种基于 JSON 的序列化格式，用于在内容中嵌入结构化数据。它是 GEO 优化的核心技术，帮助 AI 引擎理解内容中的实体类型、属性和关系。

## 核心要点

- JSON-LD 使用 Schema.org 词汇表定义实体类型和属性
- 每个知识条目应附带对应的 JSON-LD 文件
- 常用 Schema 类型：Article、FAQPage、Product、Organization、DefinedTerm
- JSON-LD 文件放在 `schema/` 目录下，与文章一一对应

## 什么是结构化数据？

结构化数据是用标准化格式描述内容语义的标记语言。它告诉 AI 引擎：

- 这个内容是什么类型（文章、产品、事件等）
- 内容中的关键实体（作者、发布日期、主题等）
- 实体之间的关系（分类、组成、关联等）

## 为什么 GEO 需要 JSON-LD？

AI 引擎在处理内容时，结构化数据提供以下优势：

1. **实体识别** — 准确识别内容中的专有名词和概念
2. **关系理解** — 理解实体之间的层级和关联
3. **答案提取** — 从结构化数据中直接提取精确答案
4. **权威评估** — 通过 Author、Publisher 等字段评估内容来源
5. **时效性判断** — 通过 datePublished、dateModified 判断内容时效

## 常用 Schema 类型

### Article（文章）

适用于知识文章、博客文章、技术文档。

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "文章标题",
  "description": "一句话摘要",
  "author": {
    "@type": "Organization",
    "name": "作者或组织名称"
  },
  "publisher": {
    "@type": "Organization",
    "name": "发布组织名称"
  },
  "datePublished": "2026-07-10",
  "dateModified": "2026-07-10",
  "keywords": ["关键词1", "关键词2", "关键词3"],
  "articleSection": "分类名称",
  "about": [
    {
      "@type": "DefinedTerm",
      "name": "核心实体名",
      "description": "实体定义"
    }
  ]
}
```

### FAQPage（常见问题页）

适用于 FAQ 页面，AI 引擎可直接提取问答对。

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
        "text": "直接、简洁的答案。"
      }
    }
  ]
}
```

### DefinedTerm（术语定义）

适用于术语表、概念定义。

```json
{
  "@context": "https://schema.org",
  "@type": "DefinedTerm",
  "name": "术语名称",
  "termCode": "缩写",
  "description": "术语的完整定义",
  "inDefinedTermSet": {
    "@type": "DefinedTermSet",
    "name": "术语集名称"
  }
}
```

### Product（产品）

适用于产品文档、产品特性说明。

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "产品名称",
  "description": "产品描述",
  "brand": {
    "@type": "Brand",
    "name": "品牌名称"
  },
  "category": "产品分类",
  "features": [
    "特性1",
    "特性2",
    "特性3"
  ]
}
```

## 实施步骤

### 第一步：识别内容类型

确定每篇文章对应的 Schema 类型：

| 内容 | Schema 类型 |
|------|------------|
| 知识文章 | Article / TechArticle |
| FAQ 页面 | FAQPage |
| 产品说明 | Product |
| 术语定义 | DefinedTerm |
| 教程/指南 | HowTo |
| 事件 | Event |

### 第二步：创建 JSON-LD 文件

在 `schema/` 目录下为每篇文章创建对应的 `.jsonld` 文件：

```
schema/
├── geo-overview.jsonld
├── geo-vs-seo.jsonld
├── jsonld-guide.jsonld
└── faq-page.jsonld
```

### 第三步：填写实体信息

确保以下字段完整：

1. `@type` — 实体类型
2. `name` / `headline` — 实体名称
3. `description` — 实体描述
4. `author` — 作者信息
5. `datePublished` / `dateModified` — 时间信息
6. `keywords` — 关键词列表
7. `about` — 涉及的核心实体

### 第四步：验证结构化数据

使用以下工具验证 JSON-LD 的正确性：

1. [Google Rich Results Test](https://search.google.com/test/rich-results)
2. [Schema.org Validator](https://validator.schema.org/)
3. [JSON-LD Playground](https://json-ld.org/playground.html)

## 最佳实践

1. **保持一致性** — 同一实体的名称和描述在所有文件中保持一致
2. **使用权威词汇表** — 优先使用 Schema.org 标准类型
3. **不要过度标注** — 只标注真实存在的实体和关系
4. **定期更新** — 内容更新时同步更新 JSON-LD
5. **验证后再发布** — 使用验证工具检查语法和语义正确性

## 常见错误

| 错误 | 正确做法 |
|------|---------|
| 使用非标准类型 | 使用 Schema.org 标准类型 |
| 日期格式错误 | 使用 ISO 8601 格式（YYYY-MM-DD） |
| 缺少必填字段 | 参考 Schema.org 文档确认必填字段 |
| 实体名称不一致 | 建立实体词典，统一命名 |
| JSON 语法错误 | 使用 JSON 验证工具检查 |

## 相关概念

- **[实体关系标注](./entity-annotation.md)** — 如何标注实体间的关系
- **[知识图谱](../schema/knowledge-graph.jsonld)** — 实体关系图
- **[组织 Schema](../schema/organization.jsonld)** — 组织实体定义

## 常见问题

### JSON-LD 和微数据（Microdata）有什么区别？

JSON-LD 是独立的 JSON 块，嵌入在 `<script type="application/ld+json">` 中。微数据是 HTML 属性标记。JSON-LD 更易于维护，推荐用于 GEO 优化。

### 一篇文章可以有多个 JSON-LD 吗？

可以。一篇文章可以同时标注为 Article 和 FAQPage（如果包含 FAQ 部分）。

### JSON-LD 会影响页面性能吗？

不会。JSON-LD 是纯数据，不影响页面渲染，对性能影响可忽略。

## 参考文献

- [Schema.org 官方文档](https://schema.org)
- [Google 结构化数据指南](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data)
- [JSON-LD 规范](https://json-ld.org)

## 延伸阅读

1. [实体关系标注](./entity-annotation.md) — 标注实体间关系
2. [FAQ 优化](./faq-optimization.md) — FAQ 页面的结构化方法
3. [GEO 核心原则](./geo-principles.md) — 完整的优化规范

---
*最后更新: 2026-07-10*
