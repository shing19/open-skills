# Open Skills

欢迎来到 Open Skills。这里公开分享可以直接安装和使用的非商业 Agent Skills。

## Skill 目录

| Skill | 用途 | 状态 |
| --- | --- | --- |
| [orchestrate-subagents](skills/orchestrate-subagents/SKILL.md) | 让主 Agent 保持干净的控制上下文，通过执行文档和有边界的 sub Agent 完成长程任务 | 可用 |
| [svg-infographic](skills/svg-infographic/SKILL.md) | 把论点、流程、比较和系统关系制作成文字可复制、布局可控的纯代码 SVG 信息图 | 可用 |

## 安装

将需要的 Skill 目录复制或链接到你的 Agent 所支持的 Skills 目录中。不同宿主的目录和能力并不相同，请先阅读对应的 `SKILL.md` 和其中引用的说明。

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

`svg-infographic` 不依赖固定模型或远程生图服务。宿主如果能够写文件并预览 SVG，就可以完成核心流程；如果不能截图或渲染，仍可输出 SVG 源码，但应明确说明尚未完成视觉验收。

## 最小用法

```text
方案已经确认。组织 sub Agent 执行：你负责调度和验收，把实现、测试和文档拆成可验收的小任务。
```

如果目标、权限、交付物或验收标准还不清楚，主 Agent 会先整理执行简报并向你确认，不会直接派发。

制作 SVG 信息图：

```text
使用 svg-infographic，把下面这段关于“反馈闭环”的说明做成一张中文信息图。
要求透明背景、文字可复制，并同时给我 SVG 源文件和 HTML 预览。
```

## 使用提示

- 先阅读目标 Skill 的 `SKILL.md`；
- 按需复制或链接整个 Skill 目录，不要只复制单个文件；
- 首次运行时按提示完成必要配置；
- 执行外部写入、部署、权限或高成本操作前，确认你的 Agent 平台会向你请求授权。

遇到问题时，可以提交 issue，并附上使用的平台、触发语、预期行为和实际结果；不要附带密钥或私人材料。

## 许可证

本仓库内容采用 [PolyForm Noncommercial License 1.0.0](LICENSE)：允许个人学习、研究、实验及其他非商业用途，但不授权商业使用。

由于该许可证限制商业用途，本仓库属于源码可见项目，不属于 OSI 定义下的开源软件；如需商业授权，请联系仓库维护者。
