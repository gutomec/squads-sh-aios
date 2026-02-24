# adaptive-tutor-k12

K-12自适应辅导专家小组。

## 概述

**adaptive-tutor-k12** 是一个完整的小组，涵盖整个个性化辅导周期：

1. **诊断评估** — 自适应诊断，映射知识空白、能力水平和学习风格
2. **课程映射** — 与BNCC/Common Core对齐的个性化学习路径，包含渐进式进阶和间隔重复
3. **自适应辅导** — 多种教学方法的个性化课程、自适应练习和即时反馈
4. **进度跟踪** — 按主题掌握度监控、停滞检测和趋势分析
5. **家长报告** — 通俗易懂的报告，庆祝成就、解释改进领域并提供实用的家庭辅导建议

**痛点：** 个别辅导可带来98%的成绩提升（相比传统课堂的20%）（Bloom, 1984），但因高昂费用大多数家庭无法负担。

## 代理

| 代理 | ID | 角色 |
|---|---|---|
| 📋 Assessor | `diagnostic-assessor` | 诊断评估和知识空白检测 |
| 🗺️ CurriculumMapper | `curriculum-mapper` | 课程映射和个性化路径 |
| 🎓 Tutor | `tutor-agent` | 自适应辅导和个性化教学 |
| 📊 ProgressTracker | `progress-tracker` | 进度跟踪和趋势分析 |
| 📧 ParentReporter | `parent-report-agent` | 家长和教育者报告生成 |

## 工作流

| 工作流 | 命令 | 描述 | 持续时间 |
|---|---|---|---|
| 完整辅导周期 | `*full-tutoring` | 完整周期：从诊断到家长报告 | 60-90分钟 |
| 快速练习 | `*quick-practice` | 快速练习：辅导加进度跟踪 | 20-40分钟 |

## 可用命令

| 命令 | 代理 | 描述 |
|---|---|---|
| `*assess-student` | Assessor | 评估学生知识水平 |
| `*identify-gaps` | Assessor | 识别特定知识空白 |
| `*map-curriculum` | CurriculumMapper | 创建个性化学习路径 |
| `*adjust-path` | CurriculumMapper | 根据进度调整路径 |
| `*tutor-session` | Tutor | 开始个性化辅导课程 |
| `*practice` | Tutor | 生成练习题 |
| `*full-tutoring` | Tutor | 完整自适应辅导周期 |
| `*track-progress` | ProgressTracker | 分析学习进度 |
| `*detect-stagnation` | ProgressTracker | 检测停滞信号 |
| `*parent-report` | ParentReporter | 生成家长进度报告 |
| `*educator-report` | ParentReporter | 生成教育者报告 |

## 快速开始

```
# 激活导师（主编排器）
/atk:agents:tutor-agent

# 完整自适应辅导周期
*full-tutoring

# 快速练习
*quick-practice

# 仅诊断评估
*assess-student

# 仅家长报告
*parent-report
```

## 目标用户

- 寻求个性化辅导的家长
- K-12学生（小学至高中）
- 教师和教育工作者
- 学校和教育机构
- 教育科技平台

## 要求

- 确定学科和年级
- 特定困难信息（可选）
- 辅导课程时间（20-90分钟）
- 未成年人数据收集的家长同意（LGPD/COPPA）
