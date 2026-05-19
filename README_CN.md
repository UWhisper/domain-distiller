<div align="center">

# Domain Distiller · 领域蒸馏器

<p align="center">
  <em>将任意领域的知识蒸馏为结构化、可决策的 Claude Code 技能的元技能</em>
</p>

> *「你想掌握的下一个领域，何必从零学起。」*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![Skills](https://img.shields.io/badge/skills.sh-Compatible-green)](https://skills.sh)

<br>

**Domain Distiller 将零散的知识转化为结构化的、可决策的 Claude Code 技能——通过正交分解、并行多智能体研究和跨源验证。**

<br>

[安装](#安装) · [工作原理](#工作原理) · [分解模式](#五大分解模式) · [不适合使用的情况](#不适合使用的情况)

<br>

[English](README.md)

</div>

---

## 安装

```bash
npx skills add UWhisper/domain-distiller
```

然后在 Claude Code 中：

```
> 把旅行规划蒸馏成一个 skill
> 把个人知识管理做成技能
> 蒸馏"如何选择消费产品"这个领域
```

蒸馏完成后，直接调用：

```
> 帮我规划 7 天东京行程，预算 1500 美元
> 帮我在 Obsidian 和 Logseq 之间做选择
> 我应该买哪台笔记本用于开发？
```

---

## 用 Domain Distiller 蒸馏的技能

Domain Distiller 已用于生成多个经过验证的技能：

| 技能 | 领域 | 安装 |
|------|------|---------|
| 🔥 **Travel Guide** | 基于五维研究的旅行规划 | `npx skills add UWhisper/travel-guide` |
| 🔥 **PKM Advisor** | 个人知识管理工具选择 | `npx skills add UWhisper/pkm-advisor` |
| **Consumer Decision** | 带约束建模的产品对比 | `npx skills add UWhisper/consumer-decision` |

每个技能都包含结构化决策框架、禁忌/风险过滤和用户偏好记忆。质量均通过裸 Claude 基线的对比验证。

---

## 工作原理

输入一个领域名称，Domain Distiller 运行七阶段流水线：

**1. 领域审计** — 这个领域值得蒸馏吗？绘制信息拓扑图。识别信号源及其可靠性。如果裸 Claude 已经能给出很好的回答，则跳过。

**2. 正交分解** — 将领域拆分为 3–5 个相互独立的维度。这是核心洞察：真正的独立性使并行研究成为可能，且不会产生冗余输出。

**3. 并行采集** — 每个维度启动一个智能体。所有研究同时进行。每个智能体独立存档其发现。

**4. 跨源验证** — 按源质量加权信号。解决来源之间的矛盾。去重重叠发现。

**5. 决策框架** — 提取 50+ 条原子的、可证伪的、领域特定的规则。构建决策树。编译为结构化的 SKILL.md。

**6. 验证** — 50 规则完整性测试。与裸 Claude 并排对比。边界情况压力测试。必须在特异性、准确性、结构性、安全性和个性化五个维度上超越基线。

**7. 打包** — 最终确定结构。作为可安装技能发布。

完整方法论见 `references/decomposition-patterns.md` 和 `references/agent-prompt-template.md`。

---

## 五大分解模式

最难也最重要的一步是将领域拆分为独立维度。从五种经过验证的模式中选择：

| 模式 | 结构 | 适用场景 | 示例 |
|------|------|----------|------|
| **情境 × 行动** | 用户处境 × 该做什么 | 推荐类问题 | 旅行规划（预算 × 目的地 × 季节） |
| **规则 × 资源** | 约束条件 × 可选方案 | 受限选择 | PKM 工具（需求 × 可用工具） |
| **原理 × 实践** | 理论 × 应用 | 技能学习 | 学习框架（概念 × 练习） |
| **静态 × 动态** | 稳定基础 × 时效信息 | 快速变化领域 | 加密投资（核心原则 × 市场数据） |
| **供给 × 需求** | 提供方 × 消费方 | 双边匹配 | 求职（候选人画像 × 市场机会） |

---

## 核心设计决策

**50 规则底线** — 一个强制函数，推动超越表面知识进入真正的领域细微差别。如果你提取不出 50 条原子的、可证伪的、领域特定的规则，这个领域可能不需要专门的技能。

**并行智能体加降级** — 智能体并行启动以追求速度。当 WebSearch 不可用时，流水线降级至训练数据并明确标注来源——对其所知和所不知保持透明。

**约束维度是强制性的** — 每个领域都有禁忌、常见错误或需要避免的事情。这个维度几乎总是蒸馏中 ROI 最高的部分。

**与裸 Claude 对比验证** — 技能必须在五个维度上产生显著更好的输出：特异性、准确性、结构性、安全性和个性化。如果不能击败基线，就没完成。

---

## 不适合使用的情况

不是每个领域都需要技能。先跑 **LLM 基线测试**：

1. 用裸 Claude 回答该领域的一个代表性问题
2. 在特异性、准确性、结构性、可操作性和安全性五个维度上评分
3. 如果已经全部优秀——蒸馏的边际价值仅来自时效性、结构化决策和偏好记忆

如果该领域缺乏以上三项附加价值维度，一个简单的 prompt 可能就足够了。

---

## 仓库结构

```
domain-distiller/
├── SKILL.md                              # 技能本体（由 Claude Code 加载）
├── README.md                             # 英文说明
├── README_CN.md                          # 中文说明（本文件）
├── references/
│   ├── decomposition-patterns.md         # 五种分解模式及多领域示例
│   ├── agent-prompt-template.md          # 维度特化 prompt 生成器
│   └── skill-output-template.md          # SKILL.md 骨架及章节指引
├── assets/
└── scripts/
```

---


## 许可证

MIT
