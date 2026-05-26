# LLM/Agent 面试知识管理助手

> 面向 LLM/Agent 领域的 AI 面试知识管理系统。它帮助你把面经、项目经历和复习材料沉淀为结构化、可行动、可长期积累的 Obsidian 知识库。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

**语言**：中文 | [English](#english-version)

## 项目概览

很多人会收集面经，但很少能真正把它们转化为自己的知识体系。本项目提供一套系统化工作流，帮助你：

1. **拆解**面试题，生成结构化、高质量、可复习的答案
2. **注入**真实项目经验，让答案带有个人区分度
3. **构建** Obsidian 双链知识图谱，支持长期积累和反复复盘

## 核心理念

每个答案都会围绕三个维度进行评估：

| 维度 | 定义 | 示例 |
|------|------|------|
| **可实操** | 读者知道第一步应该做什么 | 具体工具、指标、阈值，例如 “Cohen's Kappa < 0.6 → 重新校准” |
| **有洞察力** | 不停留在标准答案 | 第一性原理、跨领域连接、反直觉观察 |
| **有表达力** | 在有限面试时间内最大化信息密度 | 清晰结构、能引导追问的 “hook” |

## 功能

### 功能 1：面经拆解

将原始面试题转化为 6 段式结构化答案：

```text
问题分析 → 核心思路 → 详细方案 → Trade-off 分析 → 面试官视角 → 追问问题
```

核心能力：

- **双维度分类**：同时按技术领域（评测、RAG、Agent 架构等）和问题类型（方案设计、指标设计、对抗测试等）打标签
- **问题聚类**：把同一场面试中的题目组织成逻辑链条，例如 “评测方法链”：偏差验证 → 分布漂移校准 → 成本优化
- **知识图谱**：自动为被引用的概念生成骨架笔记，并通过双向链接避免悬空引用
- **小白友好 review**：每条答案链都会检查非专家读者是否能看懂，避免半年后自己也读不懂

### 功能 2：经验注入

把你的真实项目经验映射进面试答案：

```text
原始经验 → 细节抽取（指标、失败、边界）→ 匹配已有题目 → 多位置注入
```

经验可以注入到答案中的不同位置：

| 位置 | 适合内容 | 示例 |
|------|----------|------|
| 详细方案 | 实现细节 | “我们使用 256 tokens + 50 token overlap” |
| 洞察 | 反直觉观察 | “chunk 越大不一定越好……” |
| Trade-off | 真实成本和失败模式 | “这让存储成本增加了 30%” |
| 区分度 | 个人叙事 | “在我们的项目里，实际遇到的问题是……” |

**重要原则**：不编造经验。系统会明确区分 “真实踩过坑的经验” 和 “理论推演”。

## 项目结构

```text
llm-agent-interview-coach/
├── SKILL.md                          # Skill 定义：触发词、核心原则、工作流
├── references/
│   ├── answer-prompt.md              # 答案生成提示词：6 段式结构 + 质量清单
│   ├── classification.md             # 分类体系：8 个领域 + 9 类问题 + 聚类方式
│   └── experience-injection.md       # 经验注入指南：抽取、匹配、注入
├── templates/
│   ├── question-note.md              # 面试题笔记模板
│   ├── experience-note.md            # 项目经验笔记模板
│   └── moc-template.md               # Map of Content（MOC）模板
└── README.md
```

## Obsidian 知识库结构

配合 Obsidian 使用时，生成的知识库建议遵循以下结构：

```text
vault/
├── 00-MOC/                # 知识地图：总 MOC、问题簇 MOC、领域索引 MOC
├── 01-领域/               # 按技术领域组织的问题笔记
│   ├── 评测/
│   ├── RAG/
│   ├── Agent架构/
│   ├── Prompt Engineering/
│   ├── 模型训练与微调/
│   ├── 部署与推理优化/
│   └── 多模态与前沿/
├── 02-经验/               # 用户自己的项目经验笔记
└── 03-面试实战/           # 按公司/岗位组织的面试记录
```

## 标签体系

| 分类 | 标签 |
|------|------|
| 技术领域 | `#LLM` `#Agent` `#RAG` `#Fine-tuning` `#Prompt` `#评测` `#部署` `#多模态` |
| 问题类型 | `#方案设计` `#指标设计` `#对抗测试` `#根因定位` `#冲突决策` `#成本优化` `#回归测试` |
| 难度 | `#基础` `#进阶` `#深入` |
| 频率 | `#高频` `#中频` `#低频` |
| 状态 | `#已掌握` `#需复习` `#待深入` |

## 使用方式

### 前置条件

- [Obsidian](https://obsidian.md/)：用于长期存储和双链管理
- 一个可以读取本仓库 Skill 定义的 AI assistant

### 拆解一场面试

1. 把面试题提供给 AI assistant
2. assistant 按技术领域和问题类型进行分类
3. 你 review 并确认分类结果
4. assistant 逐题生成结构化答案
5. 每条答案写入 Obsidian vault 前先由你确认
6. 对答案中引用的新概念自动创建骨架笔记
7. 最后进行小白友好 review，确保整条知识链可理解

### 注入项目经验

1. 描述一段项目经验，一句话也可以
2. assistant 追问关键细节：指标、失败经历、边界条件
3. assistant 在 vault 中搜索可匹配的面试题
4. 你 review 经验注入方案
5. 确认后更新题目笔记，或创建独立经验笔记

## 设计决策

### 为什么强调 “不编造经验”？

面试里最尴尬的时刻不是 “我不会”，而是被连续追问后发现经验是编的。这个系统会严格区分真实经验和理论推演。

### 为什么要做 “小白友好 review”？

知识库的价值在于**长期积累**。如果几个月后你看不懂答案里引用的概念，知识库就失效了。每个概念都应该在 vault 内自洽、可追溯、可复习。

### 为什么选择 Obsidian？

双向链接、本地存储、原生 Markdown。面试知识需要长期积累和灵活交叉引用，Obsidian 的知识图谱和 backlinks 很适合这个场景。

## License

本项目基于 [MIT License](LICENSE) 发布。

## Contributing

欢迎贡献。你可以直接提交 Pull Request；如果是较大的改动，建议先开 issue 讨论。

---

## English Version

# LLM/Agent Interview Coach

> AI-powered interview knowledge management system for LLM/Agent domain. Transform interview experiences into a structured, actionable knowledge base in Obsidian.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

## Overview

Most people collect interview experiences ("面经") but never turn them into personal knowledge. This project bridges that gap by providing a systematic workflow to:

1. **Decompose** interview questions into structured, high-quality answers
2. **Inject** your real project experience into those answers
3. **Build** a connected knowledge graph in Obsidian for long-term accumulation

## Core Philosophy

Every answer is evaluated against three dimensions:

| Dimension | Definition | Example |
|-----------|-----------|---------|
| **Actionable** | Reader knows exactly what to do first | Specific tools, metrics, thresholds (e.g., "Cohen's Kappa < 0.6 → recalibrate") |
| **Insightful** | Goes beyond standard answers | First principles, cross-domain connections, counter-intuitive observations |
| **Expressive** | Maximizes information in limited time | Clear structure, "hooks" to guide follow-up questions |

## Features

### Feature 1: Interview Decomposition

Transform raw interview questions into structured answers with a 6-part framework:

```text
Problem Analysis → Core Approach → Detailed Solution → Trade-off Analysis → Interviewer Perspective → Follow-up Questions
```

Key capabilities:

- **Dual-dimension classification**: Questions are tagged by both technical domain (Evaluation, RAG, Agent Architecture, etc.) and question type (System Design, Metrics Design, Adversarial Testing, etc.)
- **Question clustering**: Questions from the same interview are grouped into logical chains (e.g., "Evaluation Method Chain": bias validation → distribution shift calibration → cost optimization)
- **Knowledge graph**: Auto-generated skeleton notes for referenced concepts, with bidirectional links ensuring no orphan references
- **Beginner-friendly review**: Every answer chain is verified for comprehensibility by a non-expert reader

### Feature 2: Experience Injection

Map your real project experience into interview answers:

```text
Raw experience → Detail extraction (metrics, failures, boundaries) → Match existing questions → Inject at multiple positions
```

Experience can be injected at different positions in an answer:

| Position | Best For | Example |
|----------|----------|---------|
| Detailed Solution | Implementation details | "We used 256 tokens + 50 token overlap" |
| Insight | Counter-intuitive observations | "Larger chunks don't always help..." |
| Trade-off | Real costs and failure modes | "This increased storage cost by 30%" |
| Differentiation | Personal narrative | "In our project, we encountered..." |

**Important**: Experience is never fabricated. The system explicitly distinguishes "battle-tested experience" from "theoretical speculation".

## Project Structure

```text
llm-agent-interview-coach/
├── SKILL.md                          # Skill definition (trigger words, core principles, workflows)
├── references/
│   ├── answer-prompt.md              # Answer generation prompt (6-part structure + quality checklist)
│   ├── classification.md             # Classification system (8 domains + 9 question types + clustering)
│   └── experience-injection.md       # Experience injection guide (extraction + matching + injection)
├── templates/
│   ├── question-note.md              # Interview question note template
│   ├── experience-note.md            # Project experience note template
│   └── moc-template.md               # Map of Content (MOC) template
└── README.md
```

## Obsidian Knowledge Base Structure

When used with Obsidian, the generated knowledge base follows this structure:

```text
vault/
├── 00-MOC/                # Knowledge maps (global MOC + question cluster MOC + domain index MOC)
├── 01-领域/               # Question notes organized by technical domain
│   ├── 评测/
│   ├── RAG/
│   ├── Agent架构/
│   ├── Prompt Engineering/
│   ├── 模型训练与微调/
│   ├── 部署与推理优化/
│   └── 多模态与前沿/
├── 02-经验/               # User's project experience notes
└── 03-面试实战/           # Organized by company/position
```

## Tag System

| Category | Tags |
|----------|------|
| Domain | `#LLM` `#Agent` `#RAG` `#Fine-tuning` `#Prompt` `#评测` `#部署` `#多模态` |
| Question Type | `#方案设计` `#指标设计` `#对抗测试` `#根因定位` `#冲突决策` `#成本优化` `#回归测试` |
| Difficulty | `#基础` `#进阶` `#深入` |
| Frequency | `#高频` `#中频` `#低频` |
| Status | `#已掌握` `#需复习` `#待深入` |

## How to Use

### Prerequisites

- [Obsidian](https://obsidian.md/) (for knowledge base storage)
- An AI assistant with access to the skill definitions in this repo

### Decompose an Interview

1. Provide the interview questions to your AI assistant
2. The assistant classifies each question by domain and type
3. Review and confirm the classification
4. The assistant generates structured answers one by one
5. Review each answer before it's written to your Obsidian vault
6. Skeleton notes for referenced concepts are auto-created
7. A beginner-friendly review ensures the entire chain is comprehensible

### Inject Project Experience

1. Describe a project experience (even a one-liner works)
2. The assistant asks follow-up questions for specifics: metrics, failures, boundary conditions
3. The assistant searches for matching questions in your vault
4. Review the proposed injection plan
5. Confirm to update the question notes or create standalone experience notes

## Design Decisions

### Why "Never Fabricate Experience"?

The most embarrassing moment in an interview isn't "I don't know" — it's being caught making up experience under follow-up questions. This system strictly separates real experience from theoretical reasoning.

### Why "Beginner-Friendly Review"?

A knowledge base's value lies in **long-term accumulation**. If you revisit an answer months later and can't understand the referenced concepts, the system has failed. Every concept must be self-contained within the vault.

### Why Obsidian?

Bidirectional links + local storage + native Markdown. Interview knowledge needs long-term accumulation and flexible cross-referencing — Obsidian's knowledge graph and backlinks are a natural fit.

## License

This project is released under the [MIT License](LICENSE).

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.
