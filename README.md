# 批判性思维教练 (Critical Thinking Coach)

> A Socratic-style critical thinking coach for Claude Code — 25 built-in topics, 6 training modes, bilingual (Chinese/English), zero-config, works out of the box.

[![Version](https://img.shields.io/badge/version-1.0.0-blue)](CHANGELOG.md)
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-skill-orange)](https://claude.ai/code)

---

## 中文文档

### 这是什么？

**批判性思维教练**是一个 Claude Code 技能包（Skill），它像一个苏格拉底式的私人教练——不给你答案，而是通过结构化提问、框架引导和反思推动，帮助你**自己发现思考中的盲点、假设和逻辑漏洞**。

核心工具是**问题**，而非答案。每次回应的核心任务是**推进你的思考**，而不是替你解决问题。

### 六大训练模式

| # | 模式 | 你做什么 | AI 做什么 |
|---|------|----------|-----------|
| 1 | 🔍 **论证解剖** | 提供一个论证 | 逐层拆解前提、推理、证据，帮你识别逻辑跳跃和隐含假设 |
| 2 | 💬 **苏格拉底对话** | 持有一个立场/观点 | 通过连环追问挑战你的假设，你为自己的立场辩护 |
| 3 | 🔗 **因果推理考察** | 提出一个因果主张 | 检验因果机制、混淆因素、反事实推理、外部有效性 |
| 4 | ⚖️ **决策思辨** | 面临一个决策 | 结构化审视备选方案、框架偏差、认知偏误、决策矩阵 |
| 5 | 📰 **信源可信度审查** | 看到一条信息/新闻 | 溯源、证据等级、动机分析、交叉验证 |
| 6 | 🔀 **类比推理检验** | 使用类比论证 | 检验相似性、关键差异、反类比、逻辑跳跃 |

### 四阶段工作流

```
阶段 1: 目标确认 → 选择训练模式 + 确定话题（用户确认）
           ↓
阶段 2: 结构化引导 → 按模式的提问框架层层推进对话（用户确认）
           ↓
阶段 3: 元认知反思 → 回顾思维过程，发现盲点和变化（用户确认）
           ↓
阶段 4: 评估与拓展 → AI 给出三维度结构化评估 + 延伸建议
```

### 话题来源（按优先级）

当你不自带话题时，系统按以下顺序寻找素材：

1. **你的自带话题**（最优先）
2. **个人知识库**（预留扩展接口，待对接）
3. **预置题库**（25 道跨学科讨论题，涵盖 6 大类）
4. **网络搜索**（实时热点话题）
5. **通用经典案例**（兜底）

### 安装

#### 前置条件

- [Claude Code](https://claude.ai/code) 已安装并配置完成

#### 方式一：直接克隆到 skills 目录

```bash
# 进入你的 Claude Code 项目目录
cd your-project/.claude/skills/

# 克隆本技能包
git clone https://github.com/AgrEconLab/critical-thinking-coach.git
```

#### 方式二：手动复制

1. 下载本仓库的 ZIP 文件并解压
2. 将整个 `critical-thinking-coach/` 文件夹复制到 `.claude/skills/` 目录下

目录结构应为：

```
your-project/
└── .claude/
    └── skills/
        └── critical-thinking-coach/
            ├── SKILL.md
            ├── README.md
            ├── CHANGELOG.md
            └── references/
                ├── topic-bank.md
                ├── domain-lenses.md
                ├── socratic-questioning.md
                ├── logical-fallacies.md
                └── personal-kb-config.md
```

#### 方式三：通过 settings.json 注册

如果你将技能包放在了其他位置，在 `.claude/settings.json` 中注册：

```json
{
  "skills": {
    "critical-thinking-coach": {
      "path": "/absolute/path/to/critical-thinking-coach",
      "description": "批判性思维对话教练"
    }
  }
}
```

### 使用

#### 触发方式

在 Claude Code 对话中，直接说出你的需求即可自动触发。以下任一说法均可：

- "帮我分析这个论证……"
- "挑战我的观点……"
- "评估这个因果主张……"
- "这条新闻靠谱吗？"
- "帮我做一个决策……"
- "这个类比对吗？"
- "我想训练批判性思维"

也可以显式调用：

```
/critical-thinking-coach
```

#### 自带话题（推荐）

```
用户: 帮我分析这个论证："因为大多数成功企业家都辍学了，所以大学教育对创业没用。"

AI: [自动进入模式1：论证解剖]
    你的核心结论是"大学教育对创业没用"——请先确认，这是你想表达的确切主张吗？
    如果换一种表述："大学教育不是创业成功的必要条件"，这两种表述有区别吗？
```

#### 从题库选题

```
用户: 我想训练批判性思维，但不知道讨论什么

AI: [展示六种模式 → 用户选择 → 从题库推荐匹配话题]
    你想从哪种训练开始？
    1. 🔍 论证解剖  2. 💬 苏格拉底对话  3. 🔗 因果推理考察
    4. ⚖️ 决策思辨  5. 📰 信源可信度审查  6. 🔀 类比推理检验
```

#### 对话示例

**场景：苏格拉底对话——检验"AI 将导致大规模失业"**

```
用户: AI 将导致大规模失业，这次和历史上的技术变革不一样。

AI:    好的。先澄清一个关键概念：你说的"大规模失业"，具体指失业率
       达到多少？（10%？25%？）你设想的时间跨度是多久？

用户: 25%，10 年内。

AI:    理解了。接下来我想追问你的核心假设——你说"这次不一样"，
       你能不能明确地说说，AI 与蒸汽机、电力、计算机这些
       以往的技术革命相比，根本性的不同在哪里？

用户: [思考并回答]……

AI:    [继续从替代视角、后果检验等维度追问……]

---（多轮后进入阶段 3：元认知反思）---

AI:    回顾刚才的思考过程：
       - 你最初的观点是"AI 将导致 25% 失业率"，现在有变化吗？
       - 在刚才的对话中，有没有发现自己之前忽略的假设？
```

### 预置题库分类

| 类别 | 题目数 | 示例话题 |
|------|--------|----------|
| 日常生活与决策 | 4 | 朋友圈养生贴、跳槽决策、"专家说"、兴趣班焦虑 |
| 科学与健康 | 4 | 保健品宣称、气候变化共识、屏幕时间与心理健康、基因决定论 |
| 科技与伦理 | 4 | AI 取代工作、算法推荐操控、人脸识别、自动驾驶电车难题 |
| 人文与社会 | 4 | 历史由胜利者书写、作者意图、文化相对主义、民意调查 |
| 经济与政策 | 5 | 最低工资与就业、自由贸易、市场有效性、教育回报率、读博决策 |
| 跨学科交叉 | 4 | 相关性与因果性、专家共识可靠性、模型简化、RCT 金标准 |

### 学科视角插件（可选）

如果你有特定专业背景（经济学、STEM、人文社科等），系统可以在通用提问框架之上叠加学科专属追问：

| 视角 | 额外追问示例 |
|------|-------------|
| 经济学/管理学 | "这个论证隐含假设了什么样的市场结构？如果放松假设还成立吗？" |
| 自然科学/工程 | "效应量在实际意义上算大还是小？统计显著性和实际意义是一回事吗？" |
| 人文/社会科学 | "作者所处的时代和立场，是否影响了他对这件事的判断？" |
| 日常生活 | "如果十年后回头看这个选择，你觉得自己会怎么评价？" |

> 学科视角是**可选插件**，如果你不表明背景或话题为通用话题，系统使用学科中立的通用框架，不会强加专业术语。

### 核心设计原则

| 原则 | 说明 |
|------|------|
| **苏格拉底优先** | 每次回应用问题引导，而非直接给答案 |
| **深度优先于广度** | 一次只深入一个维度，不"问题轰炸" |
| **确认门设计** | 模式选择、话题选择、训练结束三节点需确认 |
| **知识库优雅降级** | 知识库不可用时自动降级到题库/网络搜索，不报错 |
| **尊重认知负荷** | 每次提问不超过 1-2 个核心问题 |
| **语言自适应** | 检测用户首条消息语言，全程跟随 |

### 文件结构

```
critical-thinking-coach/
├── SKILL.md                         # 技能主指令（Claude Code 读取）
├── README.md                        # 本文件
├── CHANGELOG.md                     # 版本历史
├── references/
│   ├── topic-bank.md                # 25 道预置题库（6 大类）
│   ├── domain-lenses.md             # 学科视角插件（4 个视角）
│   ├── socratic-questioning.md      # 苏格拉底提问技术参考（6 类问题模板）
│   ├── logical-fallacies.md         # 常见逻辑谬误速查表（5 类）
│   └── personal-kb-config.md        # 个人知识库配置模板（预留扩展）
└── evals/
    └── evals.json                   # 测试用例（8 个）
```

### 常见问题

**Q: 我需要有批判性思维基础吗？**
A: 不需要。预置题库从日常生活类开始推荐，零门槛。AI 教练会用日常语言提问，不会预设你的专业背景。

**Q: 一次训练大概多长时间？**
A: 通常 5-8 轮对话，约 10-20 分钟。取决于话题复杂度和你的思考深度。

**Q: 我可以在训练中途切换模式吗？**
A: 可以。比如你从苏格拉底对话开始，发现自己的推理有漏洞，可以切换到论证解剖模式系统拆解。AI 会先总结前段收获，再征求你确认。

**Q: 这个技能会存储我的对话吗？**
A: 技能本身不存储对话。Claude Code 的对话记录由 Claude Code 平台自身管理。

**Q: 知识库联动功能什么时候可用？**
A: 这是预留扩展接口，需要你自行对接 MCP 知识库工具。不影响其他功能——题库和网络搜索始终可用。

---

## English Documentation

### What Is This?

**Critical Thinking Coach** is a Claude Code skill that acts as a Socratic personal trainer — it doesn't give you answers. Instead, through structured questioning, framework guidance, and reflective prompts, it helps you **discover blind spots, hidden assumptions, and logical gaps in your own thinking**.

Its core tool is **questions**, not answers. The mission of every response is to **advance your thinking**, not to solve the problem for you.

### Six Training Modes

| # | Mode | What You Do | What the AI Does |
|---|------|-------------|------------------|
| 1 | 🔍 **Argument Analysis** | Provide an argument | Layer-by-layer breakdown of premises, reasoning, evidence; identify logical leaps and hidden assumptions |
| 2 | 💬 **Socratic Dialogue** | Hold a position/view | Challenge your assumptions through sequential questioning; you defend your stance |
| 3 | 🔗 **Causal Reasoning** | Present a causal claim | Examine causal mechanisms, confounders, counterfactuals, external validity |
| 4 | ⚖️ **Decision Analysis** | Face a decision | Structured review of alternatives, framing bias, cognitive biases, decision matrix |
| 5 | 📰 **Source Credibility** | Encounter a claim/news | Trace origins, evidence levels, motive analysis, cross-verification |
| 6 | 🔀 **Analogy Check** | Use an analogy in argument | Test similarity, key differences, counter-analogies, logical leaps |

### Four-Stage Workflow

```
Stage 1: Goal Setting → Choose training mode + topic (user confirms)
           ↓
Stage 2: Structured Guidance → Layer-by-layer questioning per mode framework (user confirms)
           ↓
Stage 3: Metacognitive Reflection → Review the thinking process; discover shifts and blind spots (user confirms)
           ↓
Stage 4: Assessment & Extension → AI provides 3-dimension structured evaluation + further suggestions
```

### Topic Sources (by Priority)

When you don't bring your own topic:

1. **Your own topic** (highest priority)
2. **Personal knowledge base** (reserved extension — requires MCP tool integration)
3. **Built-in topic bank** (25 cross-disciplinary topics across 6 categories)
4. **Web search** (real-time trending topics, via `WebSearch` tool)
5. **Classic generic cases** (fallback)

### Installation

#### Prerequisites

- [Claude Code](https://claude.ai/code) installed and configured

#### Option 1: Clone directly into the skills directory

```bash
cd your-project/.claude/skills/
git clone https://github.com/AgrEconLab/critical-thinking-coach.git
```

#### Option 2: Manual copy

1. Download and extract the repository ZIP
2. Copy the `critical-thinking-coach/` folder into `.claude/skills/`

The directory structure should be:

```
your-project/
└── .claude/
    └── skills/
        └── critical-thinking-coach/
            ├── SKILL.md
            ├── README.md
            ├── CHANGELOG.md
            └── references/
                ├── topic-bank.md
                ├── domain-lenses.md
                ├── socratic-questioning.md
                ├── logical-fallacies.md
                └── personal-kb-config.md
```

#### Option 3: Register via settings.json

If you placed the skill elsewhere, register it in `.claude/settings.json`:

```json
{
  "skills": {
    "critical-thinking-coach": {
      "path": "/absolute/path/to/critical-thinking-coach",
      "description": "Critical thinking dialogue coach"
    }
  }
}
```

### Usage

#### Triggering

In a Claude Code conversation, simply express your need. Any of these will trigger the skill:

- "Help me analyze this argument..."
- "Challenge my view on..."
- "Evaluate this causal claim..."
- "Is this news reliable?"
- "Help me make a decision..."
- "Is this analogy valid?"
- "I want to train my critical thinking"

Or invoke explicitly:

```
/critical-thinking-coach
```

#### Bring Your Own Topic (Recommended)

```
User: Help me analyze this argument: "Most successful entrepreneurs
      dropped out of college, so college is useless for entrepreneurship."

AI:   [Auto-enters Mode 1: Argument Analysis]
      Your core claim is "college is useless for entrepreneurship" —
      let me first confirm: is that exactly what you mean?
      How would you distinguish this from the claim that
      "college is not a necessary condition for entrepreneurial success"?
```

#### Browse the Topic Bank

```
User: I want to practice critical thinking, but I don't know where to start.

AI:   [Shows 6 modes → user picks → recommends matching topics from bank]
      Which mode would you like to start with?
      1. 🔍 Argument Analysis    2. 💬 Socratic Dialogue
      3. 🔗 Causal Reasoning     4. ⚖️ Decision Analysis
      5. 📰 Source Credibility   6. 🔀 Analogy Check
```

#### Conversation Example

**Scenario: Socratic Dialogue — testing "AI will cause mass unemployment"**

```
User: AI will cause mass unemployment. This time is different from
      previous technological changes.

AI:   Let me start by clarifying a key concept: when you say
      "mass unemployment," what threshold do you have in mind?
      10%? 25%? And over what time horizon?

User: 25%, within 10 years.

AI:   Understood. Now let me probe your core assumption — you say
      "this time is different." Can you spell out exactly what makes AI
      fundamentally different from steam power, electricity, or computers
      as technological revolutions?

User: [Thinks and responds]...

AI:   [Continues with alternative perspectives, consequence testing...]

---(Multiple rounds later, entering Stage 3: Metacognitive Reflection)---

AI:   Let's reflect on this thinking process:
      - Your initial view was "AI will cause 25% unemployment."
        Has anything shifted?
      - Did you notice any assumptions you hadn't been aware of?
```

### Built-in Topic Bank

| Category | # Topics | Examples |
|----------|----------|----------|
| Daily Life & Decisions | 4 | Viral health advice, job-switching, "experts say," extracurricular anxiety |
| Science & Health | 4 | Supplement claims, climate consensus, screen time & mental health, genetic determinism |
| Tech & Ethics | 4 | AI replacing jobs, algorithmic manipulation, facial recognition, trolley problem |
| Humanities & Society | 4 | History written by victors, authorial intent, cultural relativism, opinion polls |
| Economics & Policy | 5 | Minimum wage & employment, free trade, market efficiency, returns to education, PhD decision |
| Cross-disciplinary | 4 | Correlation vs. causation, expert consensus reliability, model simplification, RCT gold standard |

### Domain Lenses (Optional Plugin)

If you have a specific disciplinary background (economics, STEM, humanities, etc.), the coach can layer domain-specific questions on top of the generic framework:

| Lens | Example Extra Question |
|------|------------------------|
| Economics / Management | "What market structure does this argument implicitly assume? Does it hold if you relax that assumption?" |
| Natural Sciences / Engineering | "Is the effect size practically meaningful? Statistical significance vs. practical significance — are they the same here?" |
| Humanities / Social Sciences | "Does the author's era and position affect their judgment on this matter?" |
| Daily Life | "If you look back at this decision ten years from now, how would you evaluate your current thinking?" |

> Domain lenses are **optional plugins**. If you don't disclose a background, the coach uses a discipline-neutral generic framework — no jargon imposed.

### Core Design Principles

| Principle | Description |
|-----------|-------------|
| **Socratic First** | Every response starts with a question, not an answer |
| **Depth Over Breadth** | One dimension at a time — no "question bombardment" |
| **Confirmation Gates** | Mode selection, topic selection, and training conclusion all require explicit user confirmation |
| **Graceful Degradation** | Falls back to topic bank / web search when knowledge base is unavailable — never errors out |
| **Respect Cognitive Load** | At most 1-2 core questions per turn |
| **Language-Adaptive** | Detects the language of the user's first message and follows it throughout |

### File Structure

```
critical-thinking-coach/
├── SKILL.md                         # Main skill instructions (read by Claude Code)
├── README.md                        # This file
├── CHANGELOG.md                     # Version history
├── references/
│   ├── topic-bank.md                # 25 pre-built topics (6 categories)
│   ├── domain-lenses.md             # Domain perspective plugins (4 lenses)
│   ├── socratic-questioning.md      # Socratic questioning reference (6 question types)
│   ├── logical-fallacies.md         # Logical fallacies cheat sheet (5 categories)
│   └── personal-kb-config.md        # Personal knowledge base config template (reserved)
└── evals/
    └── evals.json                   # Test cases (8 cases)
```

### FAQ

**Q: Do I need a background in critical thinking?**
A: No. The built-in topic bank starts with zero-barrier daily-life topics. The coach uses plain language and doesn't assume any disciplinary background.

**Q: How long does a training session take?**
A: Typically 5-8 rounds of dialogue, about 10-20 minutes. Depends on topic complexity and how deeply you think.

**Q: Can I switch modes mid-session?**
A: Yes. For example, if you start with Socratic Dialogue and discover a logical gap, you can switch to Argument Analysis for a systematic breakdown. The AI summarizes the previous stage and asks for your confirmation before switching.

**Q: Does this skill store my conversations?**
A: The skill itself does not store conversations. Claude Code's conversation records are managed by the Claude Code platform.

**Q: When will the knowledge base integration be available?**
A: It's a reserved extension interface — you need to integrate an MCP knowledge base tool yourself. All other features (topic bank, web search) work independently.

---

## 致谢 / Acknowledgments

- 苏格拉底提问方法论 / Socratic questioning methodology
- [Claude Code Skills](https://claude.ai/code) 平台支持

## 许可 / License

MIT
