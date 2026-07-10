# 知识库内容索引

> 所有知识条目的结构化索引，维护实体关系和内部链接。

## 知识分类

### GEO 基础

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [GEO 概述](./docs/geo-overview.md) | 高 | GEO, AI 引擎, SEO | 待创建 |
| [GEO vs SEO](./docs/geo-vs-seo.md) | 高 | GEO, SEO, 对比分析 | 待创建 |
| [GEO 核心原则](./docs/geo-principles.md) | 高 | GEO, 结构化数据, 答案优先 | 待创建 |

### 技术实现

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [JSON-LD 结构化数据](./docs/jsonld-guide.md) | 高 | JSON-LD, Schema.org | 待创建 |
| [实体关系标注](./docs/entity-annotation.md) | 中 | 实体, 知识图谱 | 待创建 |
| [FAQ 优化](./docs/faq-optimization.md) | 中 | FAQ, 自然语言 | 待创建 |

### 应用场景

| 文章 | 优先级 | 实体 | 状态 |
|------|--------|------|------|
| [RAG 知识库集成](./docs/rag-integration.md) | 中 | RAG, 向量数据库 | 待创建 |
| [产品文档 GEO](./docs/product-docs-geo.md) | 中 | 产品文档, 技术写作 | 待创建 |
| [营销内容 GEO](./docs/marketing-geo.md) | 中 | 营销, 内容营销 | 待创建 |

### 工具与资源

| 资源 | 类型 | 说明 | 状态 |
|------|------|------|------|
| [FAQ Schema](./docs/faq-schema.json) | JSON-LD | 常见问题结构化数据 | ✅ 已创建 |
| [组织 Schema](./schema/organization.jsonld) | JSON-LD | 组织实体定义 | ✅ 已创建 |
| [知识图谱](./schema/knowledge-graph.jsonld) | JSON-LD | 实体关系图 | ✅ 已创建 |
| [文章模板](./docs/_template.md) | 模板 | 新文章模板 | ✅ 已创建 |

## 实体地图

```
GEO
├── relatedTo → SEO
├── enables → RAG
├── enables → 知识图谱
└── benefits → AI 生成引擎

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

- [GEO 概述](./docs/geo-overview.md) → 链接到 [GEO vs SEO](./docs/geo-vs-seo.md), [核心原则](./docs/geo-principles.md)
- [GEO vs SEO](./docs/geo-vs-seo.md) → 链接到 [GEO 概述](./docs/geo-overview.md), [技术实现](./docs/jsonld-guide.md)
- [JSON-LD 指南](./docs/jsonld-guide.md) → 链接到 [实体标注](./docs/entity-annotation.md), [FAQ 优化](./docs/faq-optimization.md)

---
*维护说明: 新增文章后同步更新此索引*
