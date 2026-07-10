---
title: "Schema.org 结构化数据完整编写指南"
slug: "schema-guide"
description: "Schema.org 结构化数据的完整编写指南，包含 20+ 种常用 Schema 类型、每个类型的完整 JSON-LD 格式案例、嵌套结构、验证方法和常见错误。"
date: 2026-07-10
updated: "2026-07-10"
tags: ["Schema.org", "JSON-LD", "结构化数据", "GEO", "SEO"]
category: "技术实现"
entities: ["Schema.org", "JSON-LD", "结构化数据", "实体", "嵌套结构"]
priority: high
---

# Schema.org 结构化数据完整编写指南

> **Schema.org** 是结构化数据的标准词汇表，**JSON-LD** 是其最常用的序列化格式。本文提供 20+ 种常用 Schema 类型的完整编写指南，每个类型都包含可直接复制使用的格式案例。

## 核心要点

- 20+ 种常用 Schema 类型的完整 JSON-LD 格式案例
- 每种类型包含必填字段和选填字段说明
- 嵌套结构示例（实体间的关联关系）
- 验证方法和常见错误排查
- 可直接复制使用的模板

---

## 一、Schema 基础

### 什么是 Schema.org？

Schema.org 是一个由 Google、Microsoft、Yahoo 和 Yandex 联合创建的标准化词汇表，用于在网页中标注结构化数据。它定义了：

- **类型（Type）** — 实体的分类（如 Article、Product、Person）
- **属性（Property）** — 实体的特征（如 name、description、url）
- **关系（Relationship）** — 实体之间的关联

### 为什么使用 JSON-LD？

| 格式 | 优点 | 缺点 | 推荐度 |
|------|------|------|--------|
| **JSON-LD** | 独立于 HTML、易维护、Google 推荐 | 需要额外 script 标签 | ⭐⭐⭐⭐⭐ |
| Microdata | 嵌入 HTML 中 | 维护困难、代码冗长 | ⭐⭐ |
| RDFa | 支持复杂关系 | 学习曲线陡峭 | ⭐⭐ |

**Google 明确推荐使用 JSON-LD** 格式。

### JSON-LD 基本结构

```json
{
  "@context": "https://schema.org",
  "@type": "类型名称",
  "属性名": "属性值",
  "嵌套属性": {
    "@type": "嵌套类型",
    "属性名": "属性值"
  }
}
```

### 在 HTML 中使用

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "文章标题"
}
</script>
```

---

## 二、常用 Schema 类型详解

### 1. Article（文章）

**适用场景：** 博客文章、新闻文章、技术文档

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://example.com/article-url"
  },
  "headline": "文章标题",
  "description": "文章的一句话摘要",
  "image": [
    "https://example.com/thumbnail1.jpg",
    "https://example.com/thumbnail2.jpg"
  ],
  "author": {
    "@type": "Person",
    "name": "作者姓名",
    "url": "https://example.com/author"
  },
  "publisher": {
    "@type": "Organization",
    "name": "发布组织名称",
    "logo": {
      "@type": "ImageObject",
      "url": "https://example.com/logo.png",
      "width": 600,
      "height": 60
    }
  },
  "datePublished": "2026-07-10",
  "dateModified": "2026-07-10",
  "articleSection": "分类名称",
  "keywords": ["关键词1", "关键词2", "关键词3"],
  "wordCount": 1500,
  "inLanguage": "zh-CN"
}
```

**必填字段：** headline, datePublished, author, publisher
**选填字段：** description, image, keywords, articleSection

---

### 2. TechArticle（技术文章）

**适用场景：** 技术教程、开发文档、API 文档

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "技术文章标题",
  "description": "技术文章摘要",
  "author": {
    "@type": "Organization",
    "name": "技术团队名称"
  },
  "datePublished": "2026-07-10",
  "dateModified": "2026-07-10",
  "proficiencyLevel": "Beginner",
  "dependencies": ["Node.js 18+", "npm 9+"],
  "codeSample": [
    {
      "@type": "SourceCode",
      "programmingLanguage": "JavaScript",
      "text": "console.log('Hello World');"
    }
  ],
  "keywords": ["技术关键词1", "技术关键词2"]
}
```

---

### 3. FAQPage（常见问题页）

**适用场景：** FAQ 页面、问答集合

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
        "text": "直接、简洁的答案，50-200 字。首句给出结论。"
      },
      "suggestedAnswer": [
        {
          "@type": "Answer",
          "text": "补充说明或替代答案",
          "score": 85
        }
      ]
    },
    {
      "@type": "Question",
      "name": "第二个常见问题？",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "第二个问题的答案。"
      }
    }
  ]
}
```

**必填字段：** name（问题）, acceptedAnswer.text（答案）
**注意：** 每个 FAQPage 最多 30 个 Question

---

### 4. HowTo（教程/操作指南）

**适用场景：** 教程、操作指南、步骤说明

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "教程名称",
  "description": "教程描述",
  "image": "https://example.com/tutorial-thumbnail.jpg",
  "totalTime": "PT30M",
  "estimatedCost": {
    "@type": "MonetaryCost",
    "currency": "CNY",
    "value": "0"
  },
  "supply": [
    {
      "@type": "HowToSupply",
      "name": "所需材料 1"
    },
    {
      "@type": "HowToSupply",
      "name": "所需材料 2"
    }
  ],
  "tool": [
    {
      "@type": "HowToTool",
      "name": "所需工具 1"
    }
  ],
  "step": [
    {
      "@type": "HowToStep",
      "name": "步骤 1 名称",
      "text": "步骤 1 的详细说明",
      "url": "https://example.com/tutorial#step1",
      "image": "https://example.com/step1.jpg"
    },
    {
      "@type": "HowToStep",
      "name": "步骤 2 名称",
      "text": "步骤 2 的详细说明",
      "url": "https://example.com/tutorial#step2",
      "itemListElement": [
        {
          "@type": "HowToSubStep",
          "text": "子步骤 2.1"
        },
        {
          "@type": "HowToSubStep",
          "text": "子步骤 2.2"
        }
      ]
    },
    {
      "@type": "HowToTip",
      "text": "提示或注意事项"
    }
  ]
}
```

**时间格式：** PT30M = 30 分钟，PT1H = 1 小时，PT1H30M = 1 小时 30 分钟

---

### 5. Product（产品）

**适用场景：** 产品页面、产品目录

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "产品名称",
  "description": "产品描述",
  "image": [
    "https://example.com/product-1.jpg",
    "https://example.com/product-2.jpg"
  ],
  "brand": {
    "@type": "Brand",
    "name": "品牌名称"
  },
  "category": "产品分类",
  "sku": "SKU-12345",
  "mpn": "MPN-12345",
  "isbn": "978-3-16-148410-0",
  "offers": {
    "@type": "Offer",
    "url": "https://example.com/product",
    "priceCurrency": "CNY",
    "price": "299.00",
    "priceValidUntil": "2026-12-31",
    "itemCondition": "https://schema.org/NewCondition",
    "availability": "https://schema.org/InStock",
    "seller": {
      "@type": "Organization",
      "name": "卖家名称"
    },
    "shippingDetails": {
      "@type": "OfferShippingDetails",
      "shippingRate": {
        "@type": "MonetaryCost",
        "value": "10.00",
        "currency": "CNY"
      },
      "deliveryTime": {
        "@type": "ShippingDeliveryTime",
        "handlingTime": {
          "@type": "QuantitativeValue",
          "minValue": "0",
          "maxValue": "1",
          "unitCode": "DAY"
        },
        "transitTime": {
          "@type": "QuantitativeValue",
          "minValue": "2",
          "maxValue": "5",
          "unitCode": "DAY"
        }
      }
    }
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": "4.5",
    "reviewCount": "128",
    "bestRating": "5",
    "worstRating": "1"
  },
  "review": [
    {
      "@type": "Review",
      "author": {
        "@type": "Person",
        "name": "评论者姓名"
      },
      "datePublished": "2026-07-10",
      "reviewBody": "评论内容...",
      "reviewRating": {
        "@type": "Rating",
        "ratingValue": "5",
        "bestRating": "5",
        "worstRating": "1"
      }
    }
  ]
}
```

---

### 6. Organization（组织/公司）

**适用场景：** 关于我们页面、品牌介绍

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "组织名称",
  "alternateName": "组织别名",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "image": "https://example.com/office.jpg",
  "description": "组织描述",
  "foundingDate": "2020-01-01",
  "founders": [
    {
      "@type": "Person",
      "name": "创始人姓名",
      "jobTitle": "创始人兼 CEO"
    }
  ],
  "numberOfEmployees": {
    "@type": "QuantitativeValue",
    "minValue": "50",
    "maxValue": "100"
  },
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "详细地址",
    "addressLocality": "城市",
    "addressRegion": "省份",
    "postalCode": "邮编",
    "addressCountry": "CN"
  },
  "contactPoint": [
    {
      "@type": "ContactPoint",
      "telephone": "+86-10-12345678",
      "contactType": "customer service",
      "availableLanguage": ["Chinese", "English"]
    }
  ],
  "sameAs": [
    "https://weibo.com/example",
    "https://twitter.com/example",
    "https://github.com/example"
  ],
  "knowsAbout": [
    "AI 教育",
    "个性化学习",
    "智能课程推荐"
  ]
}
```

---

### 7. Person（人物）

**适用场景：** 作者页面、专家简介

```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "人物姓名",
  "givenName": "名",
  "familyName": "姓",
  "honorificPrefix": "博士",
  "honorificSuffix": "教授",
  "url": "https://example.com/person",
  "image": "https://example.com/photo.jpg",
  "jobTitle": "职位头衔",
  "worksFor": {
    "@type": "Organization",
    "name": "所属组织"
  },
  "alumniOf": [
    {
      "@type": "EducationalOrganization",
      "name": "毕业院校"
    }
  ],
  "sameAs": [
    "https://linkedin.com/in/person",
    "https://github.com/person"
  ],
  "knowsAbout": [
    "人工智能",
    "机器学习",
    "自然语言处理"
  ]
}
```

---

### 8. Event（事件/活动）

**适用场景：** 线上活动、线下会议、网络研讨会

```json
{
  "@context": "https://schema.org",
  "@type": "Event",
  "name": "活动名称",
  "description": "活动描述",
  "image": "https://example.com/event-poster.jpg",
  "startDate": "2026-08-15T09:00:00+08:00",
  "endDate": "2026-08-15T18:00:00+08:00",
  "eventAttendanceMode": "https://schema.org/OnlineEventAttendanceMode",
  "eventStatus": "https://schema.org/EventScheduled",
  "location": {
    "@type": "VirtualLocation",
    "url": "https://example.com/live-stream"
  },
  "performer": [
    {
      "@type": "Person",
      "name": "演讲者姓名"
    }
  ],
  "organizer": {
    "@type": "Organization",
    "name": "组织方名称",
    "url": "https://example.com"
  },
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "CNY",
    "url": "https://example.com/register",
    "validFrom": "2026-07-10T00:00:00+08:00",
    "availability": "https://schema.org/InStock"
  }
}
```

---

### 9. BreadcrumbList（面包屑导航）

**适用场景：** 所有页面的面包屑导航

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "首页",
      "item": "https://example.com/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "分类页",
      "item": "https://example.com/category/"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "当前文章",
      "item": "https://example.com/category/article/"
    }
  ]
}
```

---

### 10. WebSite（网站）

**适用场景：** 网站首页

```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "网站名称",
  "alternateName": "网站别名",
  "url": "https://example.com",
  "description": "网站描述",
  "inLanguage": "zh-CN",
  "publisher": {
    "@type": "Organization",
    "name": "发布组织"
  },
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://example.com/search?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
```

---

### 11. DefinedTerm（术语定义）

**适用场景：** 术语表、概念定义、GEO 实体标注

```json
{
  "@context": "https://schema.org",
  "@type": "DefinedTerm",
  "name": "术语名称",
  "termCode": "缩写",
  "description": "术语的完整定义",
  "inDefinedTermSet": {
    "@type": "DefinedTermSet",
    "name": "术语集名称",
    "description": "术语集描述",
    "url": "https://example.com/glossary"
  },
  "url": "https://example.com/term-url"
}
```

---

### 12. Dataset（数据集）

**适用场景：** 研究报告、数据报告、统计信息

```json
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "数据集名称",
  "description": "数据集描述",
  "url": "https://example.com/dataset",
  "datePublished": "2026-07-10",
  "license": "https://creativecommons.org/licenses/by/4.0/",
  "creator": {
    "@type": "Organization",
    "name": "数据创建者"
  },
  "variableMeasured": [
    {
      "@type": "PropertyValue",
      "name": "变量 1",
      "description": "变量描述"
    }
  ],
  "distribution": [
    {
      "@type": "DataDownload",
      "contentUrl": "https://example.com/data.csv",
      "encodingFormat": "text/csv"
    }
  ]
}
```

---

### 13. Course（课程）

**适用场景：** 在线课程、教育产品

```json
{
  "@context": "https://schema.org",
  "@type": "Course",
  "name": "课程名称",
  "description": "课程描述",
  "url": "https://example.com/course",
  "image": "https://example.com/course-cover.jpg",
  "provider": {
    "@type": "Organization",
    "name": "课程提供方",
    "sameAs": "https://example.com"
  },
  "hasCourseInstance": {
    "@type": "CourseInstance",
    "courseMode": "online",
    "duration": "PT10H",
    "instructor": {
      "@type": "Person",
      "name": "讲师姓名"
    }
  },
  "educationalLevel": "Intermediate",
  "audience": {
    "@type": "EducationalAudience",
    "educationalRole": "student"
  },
  "teaches": ["技能 1", "技能 2", "技能 3"],
  "about": [
    {
      "@type": "DefinedTerm",
      "name": "课程主题"
    }
  ]
}
```

---

### 14. Review（评论）

**适用场景：** 产品评测、服务评价

```json
{
  "@context": "https://schema.org",
  "@type": "Review",
  "itemReviewed": {
    "@type": "Product",
    "name": "被评测产品名称"
  },
  "author": {
    "@type": "Person",
    "name": "评论者姓名"
  },
  "datePublished": "2026-07-10",
  "reviewBody": "详细的评论内容...",
  "reviewRating": {
    "@type": "Rating",
    "ratingValue": "4.5",
    "bestRating": "5",
    "worstRating": "1"
  },
  "publisher": {
    "@type": "Organization",
    "name": "发布组织"
  }
}
```

---

### 15. VideoObject（视频）

**适用场景：** 视频教程、产品演示视频

```json
{
  "@context": "https://schema.org",
  "@type": "VideoObject",
  "name": "视频标题",
  "description": "视频描述",
  "thumbnailUrl": [
    "https://example.com/thumbnail.jpg"
  ],
  "contentUrl": "https://example.com/video.mp4",
  "embedUrl": "https://example.com/embed/video",
  "uploadDate": "2026-07-10",
  "duration": "PT5M30S",
  "interactionStatistic": {
    "@type": "InteractionCounter",
    "interactionType": "https://schema.org/WatchAction",
    "userInteractionCount": 12345
  },
  "regionsAllowed": "CN"
}
```

---

## 三、嵌套结构示例

### 复杂嵌套：文章 + 作者 + 组织

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "复杂嵌套示例",
  "author": {
    "@type": "Person",
    "name": "张三",
    "jobTitle": "首席技术官",
    "worksFor": {
      "@type": "Organization",
      "name": "智学 AI",
      "sameAs": "https://zhixueai.com"
    },
    "sameAs": [
      "https://linkedin.com/in/zhangsan"
    ]
  },
  "publisher": {
    "@type": "Organization",
    "name": "智学 AI",
    "logo": {
      "@type": "ImageObject",
      "url": "https://zhixueai.com/logo.png",
      "width": 600,
      "height": 60
    }
  },
  "about": [
    {
      "@type": "DefinedTerm",
      "name": "AI 学习",
      "description": "利用人工智能技术实现个性化学习"
    }
  ]
}
```

### 嵌套：FAQ + 产品

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "智学 AI 的个性化学习怎么样？",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "智学 AI 的个性化学习系统通过分析学习者数据，动态生成最适合的学习路径。"
      },
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "智学 AI 的个性化学习系统通过分析学习者数据，动态生成最适合的学习路径。用户数据显示学习效率提升 2-3 倍。"
      }
    }
  ]
}
```

---

## 四、验证方法

### 1. Google Rich Results Test

- 网址：https://search.google.com/test/rich-results
- 输入 URL 或粘贴 JSON-LD 代码
- 查看是否获得富媒体搜索结果资格

### 2. Schema.org Validator

- 网址：https://validator.schema.org/
- 验证 JSON-LD 语法和语义正确性
- 显示所有识别的实体和属性

### 3. JSON-LD Playground

- 网址：https://json-ld.org/playground.html
- 测试 JSON-LD 展开/压缩
- 转换为 RDF 格式

### 4. 常见错误

| 错误 | 原因 | 修复方法 |
|------|------|---------|
| `Invalid character` | JSON 语法错误 | 使用 JSON 验证器检查 |
| `Unknown type` | 使用了非标准类型 | 使用 Schema.org 标准类型 |
| `Missing required field` | 缺少必填字段 | 参考 Schema.org 文档 |
| `Invalid date format` | 日期格式不正确 | 使用 ISO 8601 格式 |
| `Invalid URL` | URL 格式错误 | 确保 URL 以 http://或https://开头 |

---

## 五、最佳实践

### 1. 每个页面至少包含的 Schema

```html
<!-- 所有页面 -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "网站名称",
  "url": "https://example.com"
}
</script>

<!-- 面包屑导航 -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [...]
}
</script>
```

### 2. 多 Schema 类型共存

一个页面可以有多个 JSON-LD 块：

```html
<!-- 网站信息 -->
<script type="application/ld+json">
{ "@context": "https://schema.org", "@type": "WebSite", ... }
</script>

<!-- 文章信息 -->
<script type="application/ld+json">
{ "@context": "https://schema.org", "@type": "Article", ... }
</script>

<!-- FAQ 信息 -->
<script type="application/ld+json">
{ "@context": "https://schema.org", "@type": "FAQPage", ... }
</script>
```

### 3. 使用 @id 建立实体关联

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@id": "https://example.com/#organization",
      "@type": "Organization",
      "name": "组织名称"
    },
    {
      "@id": "https://example.com/article/#article",
      "@type": "Article",
      "publisher": { "@id": "https://example.com/#organization" }
    }
  ]
}
```

---

## 六、Schema 类型速查表

| 类型 | 适用场景 | 必填字段 |
|------|---------|---------|
| Article | 博客、新闻 | headline, datePublished, author |
| TechArticle | 技术文档 | headline, datePublished, author |
| FAQPage | 常见问题 | mainEntity[].name, mainEntity[].acceptedAnswer |
| HowTo | 教程 | name, step[].text |
| Product | 产品页 | name, offers |
| Organization | 组织/公司 | name, url |
| Person | 人物 | name |
| Event | 活动 | name, startDate, location |
| BreadcrumbList | 面包屑 | itemListElement[] |
| WebSite | 网站 | name, url |
| DefinedTerm | 术语 | name, description |
| Course | 课程 | name, provider |
| Review | 评论 | itemReviewed, reviewRating |
| VideoObject | 视频 | name, thumbnailUrl, uploadDate |

---

## 相关概念

- **[JSON-LD 指南](./jsonld-guide.md)** — JSON-LD 基础实现
- **[实体关系标注](./entity-annotation.md)** — 实体标注方法
- **[从零开始布局 GEO](./geo-from-zero.md)** — 完整实战指南

## 常见问题

### 一个页面可以有多个 JSON-LD 吗？

可以。一个页面可以包含多个 `<script type="application/ld+json">` 块，分别标注不同的实体类型。

### JSON-LD 和 Microdata 能混用吗？

技术上可以，但不推荐。建议统一使用 JSON-LD，更易于维护和验证。

### Schema 会影响页面性能吗？

不会。JSON-LD 是纯数据，不影响页面渲染，对性能影响可忽略。

### 如何知道使用哪种 Schema 类型？

参考 [Schema.org 文档](https://schema.org/docs/documents.html)，选择最匹配内容类型的 Schema。如果不确定，使用更通用的类型（如 Article）。

## 参考文献

- [Schema.org 官方文档](https://schema.org)
- [Google 结构化数据指南](https://developers.google.com/search/docs)
- [Google Rich Results Test](https://search.google.com/test/rich-results)
- [JSON-LD 规范](https://json-ld.org)

## 延伸阅读

1. [JSON-LD 指南](./jsonld-guide.md) — 结构化数据基础
2. [从零开始布局 GEO](./geo-from-zero.md) — 完整实战指南
3. [GEO + SEO 整合策略](./geo-seo-integration.md) — 双重优化方案

---
*最后更新: 2026-07-10*
