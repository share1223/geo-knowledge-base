---
title: "实体关系标注指南"
slug: "entity-annotation"
description: "实体关系标注是 GEO 优化的核心环节，通过明确标注内容中的实体及其关系，帮助 AI 引擎构建知识图谱并准确理解内容语义。"
date: 2026-07-10
updated: 2026-07-10
tags: ["实体", "知识图谱", "标注", "GEO"]
category: "技术实现"
entities: ["实体", "知识图谱", "关系标注", "语义"]
priority: medium
---

# 实体关系标注指南

**实体关系标注**是 GEO 优化的核心环节，通过明确标注内容中的实体及其关系，帮助 AI 引擎构建知识图谱并准确理解内容语义。

## 核心要点

- 实体是内容中的关键概念、产品、人物、组织等
- 关系类型包括 isA、partOf、relatedTo、enables、conflictsWith
- 首次出现的专有名词用 **粗体** 标注
- 在 `## 相关概念` 小节列出关联实体
- 在 `knowledge-graph.jsonld` 中维护全局实体关系

## 什么是实体？

实体是内容中具有明确定义和独立意义的关键概念。例如：

| 实体类型 | 示例 |
|---------|------|
| 技术概念 | GEO、SEO、RAG、JSON-LD |
| 产品 | ChatGPT、Gemini、Perplexity |
| 组织 | Google、OpenAI、Schema.org |
| 标准/规范 | Schema.org、JSON-LD 规范 |
| 方法论 | 答案优先、结构化数据 |

## 关系类型

使用标准关系类型标注实体间的关联：

| 关系类型 | 含义 | 示例 |
|---------|------|------|
| `isA` | 分类关系 | GEO **isA** 内容优化方法 |
| `partOf` | 组成关系 | JSON-LD **partOf** 结构化数据 |
| `relatedTo` | 关联关系 | GEO **relatedTo** SEO |
| `enables` | 使能关系 | GEO **enables** RAG 检索 |
| `conflictsWith` | 冲突关系 | 方案 A **conflictsWith** 方案 B |
| `implements` | 实现关系 | JSON-LD **implements** Schema.org |
| `benefitsFrom` | 受益关系 | AI 引擎 **benefitsFrom** GEO |

## 标注方法

### 文本中标注

在 Markdown 文章中：

1. **首次出现**的专有名词用 **粗体** 标注
2. 首次出现时给出全称和定义
3. 在 `## 相关概念` 小节列出关联实体

```markdown
# 什么是 GEO？

**GEO**（Generative Engine Optimization，生成引擎优化）是一种内容优化方法。
它与 **SEO**（Search Engine Optimization）互补，两者都关注内容的可检索性。

## 相关概念

- **[SEO](./seo-overview.md)** — 搜索引擎优化，与 GEO 互补
- **[RAG](./rag-overview.md)** — 检索增强生成，GEO 提升其检索质量
```

### JSON-LD 中标注

在 `schema/knowledge-graph.jsonld` 中维护全局实体关系：

```json
{
  "@id": "#relationship-geo-seo",
  "@type": "Relationship",
  "subject": { "@id": "#geo" },
  "predicate": "relatedTo",
  "object": { "@id": "#seo" },
  "description": "GEO 与 SEO 互补，GEO 是 SEO 在 AI 时代的延伸"
}
```

## 实体词典

维护一个统一的实体词典，确保同一实体在所有文件中命名一致：

| 实体 ID | 名称 | 类型 | 定义 |
|---------|------|------|------|
| `#geo` | GEO | 方法论 | Generative Engine Optimization |
| `#seo` | SEO | 方法论 | Search Engine Optimization |
| `#rag` | RAG | 技术 | Retrieval-Augmented Generation |
| `#json-ld` | JSON-LD | 格式 | JavaScript Object Notation for Linked Data |

## 标注流程

### 第一步：识别实体

阅读内容，标记所有关键概念、产品、组织、标准。

### 第二步：确定关系

为每对相关的实体确定关系类型。

### 第三步：更新知识图谱

在 `knowledge-graph.jsonld` 中添加或更新实体和关系。

### 第四步：验证一致性

检查实体命名、定义在所有文件中是否一致。

## 最佳实践

1. **首次标注** — 每个实体在知识库中首次出现时完整定义
2. **统一命名** — 同一实体使用相同的名称和 ID
3. **关系最小化** — 只标注真正重要的关系，避免过度关联
4. **定期审查** — 每季度审查一次知识图谱的准确性
5. **使用标准** — 优先使用 Schema.org 的关系类型

## 相关概念

- **[JSON-LD 指南](./jsonld-guide.md)** — 结构化数据实现
- **[知识图谱](../schema/knowledge-graph.jsonld)** — 全局实体关系图
- **[GEO 核心原则](./geo-principles.md)** — 实体标注在 GEO 中的位置

## 常见问题

### 需要标注所有名词吗？

不需要。只标注关键概念、专有名词、产品名等有独立意义的实体。

### 关系太多怎么办？

优先标注最核心的关系（3-5 个/实体），次要关系可以省略。

### 如何维护实体词典？

在 `sitemap.md` 或独立的实体词典文件中维护，新增实体时同步更新。

## 参考文献

- [Schema.org Relationship](https://schema.org/Relationship)
- [Schema.org DefinedTerm](https://schema.org/DefinedTerm)

## 延伸阅读

1. [JSON-LD 指南](./jsonld-guide.md) — 结构化数据实现
2. [FAQ 优化](./faq-optimization.md) — 自然语言提问覆盖
3. [GEO 核心原则](./geo-principles.md) — 完整的优化框架

---
*最后更新: 2026-07-10*
