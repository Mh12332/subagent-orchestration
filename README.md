# Codex 子代理调度 · Subagent Orchestration

为 Codex 提供一套**先比较方案、再经用户确认、最后委派和复核**的多代理协作流程。适用于并行核验、论文关键结论复核和需要独立意见的任务。

A Codex skill for comparing delegation plans, getting explicit approval, and reconciling independent work. The instructions and templates are written in Chinese.

[快速安装](#快速安装) · [使用示例](#使用示例) · [仓库文件](#仓库文件) · [版本发布](https://github.com/Mh12332/subagent-orchestration/releases)

## 工作流程

1. **判断是否值得委派。** 有明确的并行收益、需要独立交叉核验，或用户要求分别形成独立意见时，先拟案。简单任务由主代理直接完成。
2. **比较并确认。** 主代理列出每档的分工、模型、推理强度、验收标准及相对开销。用户看到完整配置后，可以在聊天中回复档位字母、名称或调整建议。
3. **执行并复核。** 按确认的配置启动子代理。主代理根据原始证据处理分歧，并报告实际使用的子代理、核验结果与局限。关键配置或范围变更时重新确认。

| 回复 | 档位 | 适用场景 |
| --- | --- | --- |
| A | 经济档 | 任务可清楚拆分，优先控制调用和重复工作 |
| B | 标准档 | 多类工作并行，关键结果需要额外核验 |
| C | 严谨档 | 重要结论需要交叉验证、反证审查或更深的证据复核 |

档位不绑定固定的子代理数量、模型或推理强度。具体配置以本次方案为准。

## 快速安装

需要支持子代理的 Codex 环境。个人安装可执行：

```sh
git clone https://github.com/Mh12332/subagent-orchestration.git ~/.agents/skills/subagent-orchestration
```

Windows PowerShell：

```powershell
git clone https://github.com/Mh12332/subagent-orchestration.git (Join-Path $HOME '.agents/skills/subagent-orchestration')
```

也可以手动复制 `SKILL.md` 和 `references/plan-template.md`，保留目录结构。仅在某个项目使用时，放入该项目的 `.agents/skills/subagent-orchestration/`。

**可选的全局入口。** 将 [AGENTS.example.md](AGENTS.example.md) 中的段落追加到现有的 `~/.codex/AGENTS.md`，让 Codex 在接到任务时主动评估委派收益。也可直接在聊天中输入 `$subagent-orchestration` 手动调用。技能发现与运行条件见 [Codex 技能指南](https://learn.chatgpt.com/docs/build-skills) 和 [Codex 子代理指南](https://learn.chatgpt.com/docs/agent-configuration/subagents)。

## 使用示例

**两包资料并行核验**

> 我有两包彼此独立的实验记录。请分别核查拉伸数据的单位换算和 EBSD 记录的筛选口径，再合并成一张修正清单。控制开销。

**定稿前独立复核**

> 我想听两份互不参考的意见。一份复算摘要里的关键数字，另一份检查证据能否支撑结论。请各自形成意见，再由你汇总。

看到方案后可以回复「A，经济档」或确认调整后的具体配置。用量估计以相对比较为主，是否适合委派取决于任务复杂度、可靠性要求和当前环境。普通的多角度分析也可由主代理直接完成。

## 仓库文件

| 文件 | 用途 |
| --- | --- |
| [SKILL.md](SKILL.md) | 技能入口、触发判断与执行规则 |
| [references/plan-template.md](references/plan-template.md) | 三档比较、任务分工和交付模板 |
| [AGENTS.example.md](AGENTS.example.md) | 可追加到个人全局指令的接入示例 |

欢迎通过 [Issues](https://github.com/Mh12332/subagent-orchestration/issues) 反馈触发不足、过度委派或配置选择的问题。复现时请使用虚构或已公开的数据。
