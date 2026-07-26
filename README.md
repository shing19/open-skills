# Open Skills

欢迎来到 Open Skills。这里收录可以直接安装和使用的 Agent Skills。

## Skill 目录

| Skill | 用途 | 状态 |
| --- | --- | --- |
| [orchestrate-subagents](skills/orchestrate-subagents/SKILL.md) | 让主 Agent 保持干净的控制上下文，通过执行文档和有边界的 sub Agent 完成长程任务 | 可用 |

## 安装

将需要的 Skill 目录复制或链接到你的 Agent 所支持的 Skills 目录中。不同宿主的目录和 sub Agent 能力并不相同，请先阅读该 Skill 的 `SKILL.md` 与 `references/setup.md`。

以 `orchestrate-subagents` 为例：

```text
open-skills/skills/orchestrate-subagents/
```

首次使用时，Skill 会在宿主支持的范围内确认：

- 低复杂度任务使用的模型和思考等级；
- 中复杂度任务使用的模型和思考等级；
- 高风险任务的处理方式；
- 最大并发数和待验收任务上限。

模型名称和可用能力取决于你的 Agent 平台；Skill 不要求使用某个固定模型。

## 最小用法

```text
方案已经确认。组织 sub Agent 执行：你负责调度和验收，把实现、测试和文档拆成可验收的小任务。
```

如果目标、权限、交付物或验收标准还不清楚，主 Agent 会先整理执行简报并向你确认，不会直接派发。

## 使用提示

- 先阅读目标 Skill 的 `SKILL.md`；
- 按需复制或链接整个 Skill 目录，不要只复制单个文件；
- 首次运行时按提示完成必要配置；
- 执行外部写入、部署、权限或高成本操作前，确认你的 Agent 平台会向你请求授权。

遇到问题时，可以提交 issue，并附上使用的平台、触发语、预期行为和实际结果；不要附带密钥或私人材料。

## 许可证

本仓库内容采用 [MIT License](LICENSE)。
