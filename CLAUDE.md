# CLAUDE.md — Critical Thinking Coach (Internal Developer Docs)

> Target audience: maintainers, contributors, and future-you.  
> User docs: `README.md` | AI instructions: `SKILL.md` | Version history: `CHANGELOG.md`

---

## Design Philosophy

### Why Socratic, Not Expert

Most AI coaching tools take an *expert stance*: diagnose the user's flaw, prescribe the fix. We take a *Socratic stance*: the user already has the capacity to reason well—our job is to slow them down enough to exercise it.

Three corollaries follow:
1. **Every response starts with a question, never a conclusion.** If you find yourself about to write "你的论证的问题是..." ("the problem with your argument is..."), stop and reframe as a question.
2. **One dimension per turn.** Question-bombing (challenging premises + evidence + logic all at once) is the most common failure mode. Depth over breadth.
3. **Confirmation gates are non-negotiable.** Mode selection, topic selection, and training conclusion must be user-confirmed. Mode switching also requires a gate.

### Why Structured, Not Open-Ended

A free-form Socratic dialogue is fun but unmemorable. The 4-stage loop (Goal → Guidance → Reflection → Assessment) ensures every session produces a *traceable shift in thinking*, not just an interesting chat.

---

## Directory Conventions

```
critical-thinking-coach/
├── SKILL.md              # AI runtime instructions (the skill itself)
├── CLAUDE.md             # This file — internal developer docs
├── README.md             # User-facing: install, usage, FAQ (bilingual)
├── CHANGELOG.md          # Semantic versioning history
├── .gitignore            # Excludes promo materials, OS/editor junk
├── references/           # Documents loaded on-demand by the AI (see loading rules)
│   ├── topic-bank.md     # 25 pre-built topics × 6 categories
│   ├── domain-lenses.md  # 4 disciplinary perspective plugins
│   ├── socratic-questioning.md  # Question-type taxonomy (6 types)
│   ├── logical-fallacies.md     # Fallacy cheat sheet (5 categories)
│   └── personal-kb-config.md    # Reserved extension (not yet active)
└── evals/
    └── evals.json        # 15 test cases × 5 categories
```

### Reference Loading Rules (from SKILL.md)

| Scenario | Load |
|----------|------|
| User has no topic | `topic-bank.md` |
| User discloses professional background | `domain-lenses.md` |
| User stuck / need question inspiration | `socratic-questioning.md` |
| Fallacy identification needed (modes 1/2/3) | `logical-fallacies.md` |
| Knowledge-base MCP tool integrated (reserved) | `personal-kb-config.md` |

**Never load all references at once.** Each document is ~2-5K tokens; loading all five wastes context for zero benefit.

---

## Extension Guide

### How to Add a New Training Mode

1. Add a row to the mode-selection menu in SKILL.md (the bilingual 6-item list in Stage 1)
2. Add a full section under `## 六大训练模式` with:
   - **适用场景**: 1-2 sentences
   - **提问框架**: 5 layers/rounds, each with 2-3 concrete question templates
   - **🎯 学科视角（可选）**: reference `domain-lenses.md` or note if not applicable
3. If the mode benefits from domain lenses, add entries in `domain-lenses.md` for all 4 perspectives (or document why not)
4. Add at least 3 topics in `topic-bank.md` listing the new mode in `适用模式`
5. Add at least 1 routing eval in `evals/evals.json` (`mode-routing-*`)
6. Update `README.md` mode table (CN + EN)

### How to Add a New Topic

1. Add entry in `references/topic-bank.md` under the appropriate category:
   - `### 话题 N：...`
   - `- **摘要**：...` (1 sentence)
   - `- **切入点**：...` (1-2 key angles)
   - `- **适用模式**：...` (1-3 applicable modes)
   - `- **推荐轮次**：...` (range, e.g., 5-7)
2. If adding a 26th+ topic, update the README count

### How to Add a New Domain Lens

1. Add a section under `## 视角五：...` in `domain-lenses.md`
2. Provide entries for all 4 core modes (论证解剖, 苏格拉底对话, 因果推理考察, 决策思辨). Modes 5 (信源可信度审查) and 6 (类比推理检验) are intentionally excluded—they are cross-disciplinary by nature
3. Add a row to the domain-lens table in README (CN + EN)

### How to Add a New Eval Case

1. Append to `evals/evals.json` `test_cases` array
2. Required fields: `id`, `category`, `description`, `expected` (or `expected_mode`), `assertions`
3. Categories: `trigger_accuracy`, `mode_routing`, `edge_case`, `domain_lens`, `antipattern`, `workflow`
4. Validate JSON: `python -m json.tool evals/evals.json`

---

## Contribution Rules

- **Language**: SKILL.md and reference docs are primarily Chinese (the skill's native language), with English in designated bilingual blocks. README is full bilingual. CLAUDE.md and CHANGELOG.md are Chinese or English at the author's discretion.
- **Naming**: Use kebab-case for directories and filenames. Use descriptive Chinese names for modes and topics.
- **No dead code**: If a topic is removed from `topic-bank.md`, remove its domain-lens cross-reference if any. If a mode is deprecated, update all affected files.
- **Evals required**: Any change to mode logic, topic routing, or anti-pattern rules must be accompanied by a new or updated eval case.
- **Commit style**: Semantic prefix (`Feat:`, `Fix:`, `Docs:`, `Chore:`, `Refactor:`) + concise description.

---

## Known Limitations & Roadmap

### v1.0.0 Limitations

| Limitation | Mitigation |
|------------|------------|
| Personal knowledge-base integration is a reserved stub | Falls back gracefully to topic bank / web search |
| Domain lenses only cover 4 perspectives | Modes 5/6 are intentionally cross-disciplinary; new lenses can be added as needed |
| Eval suite is specification-only (no automated runner) | JSON schema is validated; manual behavioral testing supplements |
| No session persistence across conversations | Each session is self-contained; the 4-stage loop ensures closure within one session |
| Topic bank is static (25 topics) | Web search fallback provides dynamic content; users can bring their own topics |

### Potential v1.1 Directions

- Automated eval runner (assertion-based, simulating user inputs)
- Knowledge-base MCP integration (activate `personal-kb-config.md`)
- Session summary export (structured reflection output)
- Additional domain lenses (law, medicine, education)

---

*This document is for internal development use. It is not loaded by the AI at runtime (only `SKILL.md` is).*
