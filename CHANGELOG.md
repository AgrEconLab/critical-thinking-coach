# CHANGELOG

## [1.0.0] — 2026-07-06

### Added
- 初始版本：六大训练模式（论证解剖、苏格拉底对话、因果推理考察、决策思辨、信源可信度审查、类比推理检验）
- 四阶段工作流（目标确认 → 结构化引导 → 元认知反思 → 评估与拓展）
- 25 道跨学科预置题库（`references/topic-bank.md`）
- 四大学科视角插件（`references/domain-lenses.md`）
- 苏格拉底提问技术参考（`references/socratic-questioning.md`）
- 常见逻辑谬误速查表（`references/logical-fallacies.md`）
- 知识库联动预留扩展接口（`references/personal-kb-config.md`）
- 反模式速查 + 好/坏回应对比示例
- 参考文档按需加载规则表
- `evals/` 测试系统（8 个用例）

### Fixed
- 虚构 API 引用（`search(source="web")` / `search(source="kb")` / `fetch(type="media_id")`）替换为 `WebSearch` 工具，知识库联动标记为预留扩展接口
- 模式切换增加确认门规则
- `domain-lenses.md` 读取时机以触发规则明确化
- **语言规则提升为最高优先级**：从原则 #6 提升为独立的顶层规则（概述之后、教练原则之前），中英双语写明，反模式表新增"语言不匹配"条目。修复英文提问→中文回复的 bug
