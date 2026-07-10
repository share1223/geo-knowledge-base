# 知识库内容索引

> 所有知识条目的结构化索引，维护实体关系和内部链接。

## 知识分类

### GEO 基础

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [GEO 概述](./docs/geo-overview.md) | 高 | GEO, AI 引擎, SEO | ✅ 已完成 |
| [GEO vs SEO](./docs/geo-vs-seo.md) | 高 | GEO, SEO, 对比分析 | ✅ 已完成 |
| [GEO 核心原则](./docs/geo-principles.md) | 高 | GEO, 结构化数据, 答案优先 | ✅ 已完成 |

### 技术实现

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [JSON-LD 结构化数据](./docs/jsonld-guide.md) | 高 | JSON-LD, Schema.org | ✅ 已完成 |
| [实体关系标注](./docs/entity-annotation.md) | 中 | 实体, 知识图谱 | ✅ 已完成 |
| [FAQ 优化](./docs/faq-optimization.md) | 中 | FAQ, 自然语言 | ✅ 已完成 |
| [Schema 完整编写指南](./docs/schema-guide.md) | 高 | Schema.org, JSON-LD, 20+ 类型, 格式案例 | ✅ 已完成 |

### 实战案例

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [从零开始布局 GEO](./docs/geo-from-zero.md) | 高 | GEO, SEO, 品牌曝光, 内容策略 | ✅ 已完成 |
| [标题与内容策略](./docs/title-content-strategy.md) | 高 | 标题优化, 内容策略, 品牌植入 | ✅ 已完成 |
| [GEO + SEO 整合策略](./docs/geo-seo-integration.md) | 高 | GEO, SEO, 整合优化, 实施路线图 | ✅ 已完成 |

### 待扩展

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [RAG 知识库集成](./docs/rag-integration.md) | 中 | RAG, 向量数据库 | 待创建 |
| [产品文档 GEO](./docs/product-docs-geo.md) | 中 | 产品文档, 技术写作 | 待创建 |
| [营销内容 GEO](./docs/marketing-geo.md) | 中 | 营销, 内容营销 | 待创建 |

### 工具与资源

| 资源 | 类型 | 说明 | 状态 |
|------|------|------|------|
| [FAQ Schema](./docs/faq-schema.json) | JSON-LD | 常见问题结构化数据 | ✅ 已完成 |
| [组织 Schema](./schema/organization.jsonld) | JSON-LD | 组织实体定义 | ✅ 已完成 |
| [知识图谱](./schema/knowledge-graph.jsonld) | JSON-LD | 实体关系图 | ✅ 已完成 |
| [文章模板](./docs/_template.md) | 模板 | 新文章模板 | ✅ 已完成 |

## 实体地图

```
GEO
├── relatedTo → SEO
├── enables → RAG
├── enables → 知识图谱
├── enables → 品牌曝光
└── benefits → AI 生成引擎

SEO
├── relatedTo → GEO
├── enables → 自然搜索流量
└── relatedTo → 关键词排名

内容策略
├── partOf → GEO
├── partOf → SEO
└── includes → 标题优化

JSON-LD
└── implements → Schema.org

AI 生成引擎
├── ChatGPT
├── Gemini
├── Perplexity
├── Claude
└── 通义千问
```

## 链接关系

- [GEO 概述](./docs/geo-overview.md) → [GEO vs SEO](./docs/geo-vs-seo.md), [核心原则](./docs/geo-principles.md), [从零开始布局 GEO](./docs/geo-from-zero.md)
- [GEO vs SEO](./docs/geo-vs-seo.md) → [GEO 概述](./docs/geo-overview.md), [JSON-LD 指南](./docs/jsonld-guide.md), [GEO + SEO 整合策略](./docs/geo-seo-integration.md)
- [JSON-LD 指南](./docs/jsonld-guide.md) → [实体标注](./docs/entity-annotation.md), [FAQ 优化](./docs/faq-optimization.md)
- [从零开始布局 GEO](./docs/geo-from-zero.md) → [核心原则](./docs/geo-principles.md), [标题与内容策略](./docs/title-content-strategy.md), [GEO + SEO 整合策略](./docs/geo-seo-integration.md)
- [标题与内容策略](./docs/title-content-strategy.md) → [从零开始布局 GEO](./docs/geo-from-zero.md), [GEO + SEO 整合策略](./docs/geo-seo-integration.md)
- [GEO + SEO 整合策略](./docs/geo-seo-integration.md) → [从零开始布局 GEO](./docs/geo-from-zero.md), [标题与内容策略](./docs/title-content-strategy.md)

---
*维护说明: 新增文章后同步更新此索引 | 最后更新: 2026-07-10*
