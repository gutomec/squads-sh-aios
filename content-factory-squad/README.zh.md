# content-factory-squad

营销内容规模化生产专家小组。

## 概述

**content-factory-squad** 是一个完整的小组，涵盖整个内容生产流水线：

1. **编辑规划** — 多渠道编辑日历、主题定义、买家旅程映射和内容支柱
2. **长篇内容创作** — 文章、博客帖子、白皮书、电子书和案例研究，针对SEO优化并具有故事性
3. **社交媒体适配** — 将长篇内容转化为Instagram轮播、Twitter/X线程、LinkedIn帖子和TikTok脚本
4. **图片简报** — 视觉方向，包含尺寸规格、构图、风格和AI生成提示词
5. **多渠道排期** — 按平台在最佳时间安排发布，管理队列和节奏

**痛点：** 为多个渠道规模化生产高质量内容需要战略、写作、设计和发布之间的协调——通常需要数天的过程可以通过智能体编排来加速。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 📋 Strategist | `content-strategist` | 内容策略师和编辑规划 |
| ✍️ Writer | `long-form-writer` | 长篇内容写作和SEO |
| 📱 SocialAdapter | `social-media-adapter` | 社交媒体内容适配器 |
| 🎨 ImageBriefer | `image-brief-generator` | 图片简报和视觉方向生成器 |
| ⏰ Scheduler | `publishing-scheduler` | 多渠道发布排期器 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整内容流水线 | `*content-pipeline` | 完整流水线：从规划到排期 | 60-120分钟 |
| 快速社交发布 | `*social-blast` | 快速生产：从主题到排期帖子 | 15-30分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*plan-calendar` | Strategist | 规划月度/季度编辑日历 |
| `*content-pipeline` | Strategist | 完整内容生产流水线 |
| `*write-article` | Writer | 撰写文章或博客帖子 |
| `*write-whitepaper` | Writer | 撰写白皮书或电子书 |
| `*adapt-social` | SocialAdapter | 适配社交媒体内容 |
| `*create-thread` | SocialAdapter | 创建Twitter/X线程 |
| `*generate-brief` | ImageBriefer | 生成内容图片简报 |
| `*batch-briefs` | ImageBriefer | 批量生成图片简报 |
| `*schedule` | Scheduler | 安排内容发布 |
| `*optimize-times` | Scheduler | 优化发布时间 |

## 快速开始

```
# 激活策略师（主编排器）
/cfs:agents:content-strategist

# 完整内容生产流水线
*content-pipeline

# 快速社交发布
*social-blast

# 仅撰写文章
*write-article

# 仅适配社交媒体
*adapt-social
```

## 目标用户

- 内容营销经理
- 社交媒体经理
- 内容策略师
- 文案和撰稿人
- 数字营销经理

## 要求

- 访问博客平台（WordPress、HubSpot、Ghost）
- 访问社交媒体工具（Buffer、Hootsuite、Later）
- 定义的品牌指南（语调、颜色调色板）
- 映射的买家角色
