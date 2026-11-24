# Codex 子代理调度技能

`subagent-orchestration` 帮助 Codex 判断任务是否值得委派，为多代理协作提供经济、标准和严谨三档方案，并在用户确认具体配置后启动子代理。

## 何时使用

- 多项工作可以并行，委派能明显提高效率或质量。
- 关键结论值得独立复算、交叉核验或反向审查。
- 用户明确要求多人独立出意见，再由主代理汇总。

简单任务由主代理直接处理。子代理数量、模型和推理强度随任务确定。环境须支持 Codex 子代理。

## 安装

把仓库中的 [SKILL.md](SKILL.md) 和 [references/plan-template.md](references/plan-template.md) 放在同一个名为 `subagent-orchestration` 的目录中，保留 `references/` 层级。将该目录放入个人技能目录 `~/.agents/skills/`，或项目的 `.agents/skills/`。

如希望 Codex 在接到任务时主动判断是否委派，将 [AGENTS.example.md](AGENTS.example.md) 的内容追加到全局 `~/.codex/AGENTS.md`。新对话中也可以用 `$subagent-orchestration` 手动调用。

## 使用示例

> 定稿前，我想听两份互不参考的意见。一份复算关键数据，另一份检查证据能否支撑结论。请各自形成意见，再由你汇总。

Codex 会在正文列出各档的分工、模型、推理强度和相对开销。看过具体方案后，回复 **A 选经济档、B 选标准档、C 选严谨档**，或说明你想调整的配置。确认后，主代理按获批方案委派、复核并汇总。
