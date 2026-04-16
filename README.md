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

```
Problem Analysis → Core Approach → Detailed Solution → Trade-off Analysis → Interviewer Perspective → Follow-up Questions
```

Key capabilities:
- **Dual-dimension classification**: Questions are tagged by both technical domain (Evaluation, RAG, Agent Architecture, etc.) and question type (System Design, Metrics Design, Adversarial Testing, etc.)
- **Question clustering**: Questions from the same interview are grouped into logical chains (e.g., "Evaluation Method Chain": bias validation → distribution shift calibration → cost optimization)
- **Knowledge graph**: Auto-generated skeleton notes for referenced concepts, with bidirectional links ensuring no orphan references
- **Beginner-friendly review**: Every answer chain is verified for comprehensibility by a non-expert reader

### Feature 2: Experience Injection

Map your real project experience into interview answers:

```
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

```
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

```
vault/
├── 00-MOC/                # Knowledge maps (global MOC + question cluster MOC + domain index MOC)
├── 01-领域/                # Question notes organized by technical domain
│   ├── 评测/
│   ├── RAG/
│   ├── Agent架构/
│   ├── Prompt Engineering/
│   ├── 模型训练与微调/
│   ├── 部署与推理优化/
│   └── 多模态与前沿/
├── 02-经验/                # User's project experience notes
└── 03-面试实战/            # Organized by company/position
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
