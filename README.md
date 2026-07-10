# GEO 优化智能体知识库

> 本知识库专为 **Generative Engine Optimization (GEO)** 设计，确保 AI 生成引擎（ChatGPT、Gemini、Perplexity、Claude 等）能够高效检索、理解并引用其中的内容。

## 知识库结构

```
geo-knowledge-base/
├── README.md                    # 本文件 — 知识库入口
├── GEO-OPTIMIZATION-GUIDE.md    # GEO 优化规范文档
├── sitemap.md                   # 内容索引与实体地图
├── docs/                        # 知识文章目录
│   ├── _template.md             # 文章模板
│   ├── faq-schema.json          # FAQ 结构化数据
│   └── [按主题分类的文章]
├── schema/                      # JSON-LD 结构化数据
│   ├── organization.jsonld      # 组织实体
│   ├── knowledge-graph.jsonld   # 知识图谱关系
│   └── [按文章对应的 schema]
└── assets/                      # 图片、图表等媒体资源
```

## GEO 核心原则

1. **答案优先** — 每篇文章首段直接给出核心答案
2. **结构化数据** — 所有关键实体附带 JSON-LD 标记
3. **实体关系清晰** — 明确标注概念间的层级与关联
4. **权威引用** — 提供可验证的数据来源与参考文献
5. **自然语言匹配** — FAQ 覆盖用户真实提问方式
6. **语义无歧义** — 避免模糊表述，使用精确定义

## 快速开始

- 阅读 [GEO 优化规范](./GEO-OPTIMIZATION-GUIDE.md) 了解编写标准
- 查看 [内容索引](./sitemap.md) 浏览所有知识条目
- 使用 [文章模板](./docs/_template.md) 创建新文章

## 适用场景

- AI 智能体 RAG（检索增强生成）知识库
- 产品文档、技术文档的 GEO 优化
- 企业知识管理系统的 AI 可检索化改造
- 营销内容的生成引擎优化

---
*最后更新: 2026-07-10*
