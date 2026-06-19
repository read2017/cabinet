# 人生内阁团 Life Cabinet

> [English README](./README.en.md)

<p align="center">
  <img src="./life-cabinet/assets/人生内阁封面.png" alt="人生内阁团封面" width="260" />
</p>

> 把重大人生决策从“一句 AI 建议”，升级成一次有追问、有分歧、有红队、有报告沉淀的 AI 董事会。

`life-cabinet` 是一个中文 agent skill，适用于 Codex、Claude Code、Gemini CLI、Cursor 等支持技能、规则或上下文扩展的主流智能体工具。它不是简单让 AI 扮演几位顾问轮流发言，而是把一次咨询组织成一套严肃的决策流程：先做决策定义访谈，冻结本次上下文，再让不同顾问基于同一事实独立写 memo，最后通过红队审查、交叉质询和秘书长裁决形成结论。

它特别适合那些“不能只听一个建议”的问题：

- 职业选择：跳槽、转行、晋升、离职、个人品牌。
- 事业判断：创业、副业、商业模式、合伙、内容商业化。
- 重大人生决策：换城市、长期规划、家庭责任、生活方式取舍。
- 风险审查：合同、现金流、投资风险、执行阻力、方案盲点。
- 阶段复盘：月度、季度、年度人生董事会复盘。

## 特性

- **先问清楚，再开会**：重大决策前必须完成决策定义访谈。信息不足时，Agent 不会急着给结论，而是先追问会改变判断的关键问题。
- **冻结上下文**：开会前会明确列出已知事实、核心假设、未知信息、备选方案和决策门槛，避免分析过程中偷换问题。
- **成员 memo，不是角色表演**：关键成员必须基于同一份上下文写独立报告，包括理由链、风险、反事实、阈值和 30 天行动。
- **红队和交叉质询**：高风险决策强制加入红队审查官，并通过交叉质询暴露最脆弱的假设。
- **默认交付完整文件包**：模式 1 和模式 2 都默认生成 HTML 报告、会议记录、分析备忘录和成员报告目录，适合复盘、打印和归档。
- **可升级真实多代理**：默认由当前 Agent 深度模拟内阁流程；用户明确要求时，可使用真实 Subagent 模式派出成员独立分析。
- **长期用户档案**：支持建立用户档案，但只提取与本次决策相关的信息，并严格区分用户事实和 AI 推断。
- **专业边界清晰**：法律、医疗、税务、投资和心理健康议题只做风险识别、问题清单和咨询准备。

## 你会得到什么

一次完整的 life-cabinet 咨询通常会产出：

- 一个对话框摘要：先给你能立即读懂的结论、关键风险和下一步。
- 一份 HTML 报告：可直接用浏览器打开，也适合打印或转成 PDF。
- 多份成员报告：人生战略、职业/商业、财务风险、法律风险、温和教练、红队等按需参与。
- 一份会议记录：保留第一轮独立意见、关键分歧、交叉质询和红队挑战。
- 一份秘书长分析备忘录：把成员分歧整合成可执行判断、成立条件和触发重算信号。

## 执行模式

`life-cabinet` 支持两种执行模式：

| 模式 | 适合场景 | 说明 |
| --- | --- | --- |
| 模式 1：深度会议模式 | 默认使用，适合绝大多数智能体工具 | 由当前 Agent 作为内阁秘书长，在同一上下文中完成追问、冻结上下文、成员 memo、红队审查、交叉质询和最终综合。 |
| 模式 2：真实 Subagent 模式 | 当你的 Agent 支持 Subagent、多代理或任务委派时使用 | 内阁秘书长会把关键成员分别派发给子代理独立分析，再汇总分歧、组织二轮质询并生成最终报告。 |

如果你的智能体环境支持 Subagent，可以在提示词里明确写：

```text
Use $life-cabinet 使用模式 2：真实 Subagent 模式，召集人生内阁团分析这个重要决策。
```

如果当前环境不支持 Subagent，Skill 会说明限制，并降级为模式 1。无论使用模式 1 还是模式 2，重大决策都会默认生成 HTML 报告和完整文件包。

## 安装

使用 `skills` CLI 从 GitHub 安装：

```bash
npx skills add read2017/cabinet
```

安装后，重启或刷新你的智能体工具，即可通过 `$life-cabinet` 触发。

也可以手动复制 `life-cabinet/` 目录到目标智能体的 skills、rules 或上下文扩展目录。Skill 的入口文件是 `SKILL.md`，界面元数据在 `agents/openai.yaml`。

## 快速开始

```text
Use $life-cabinet 召集人生内阁团，帮我分析这个决策：

我要不要从大厂离职，做自己的 AI 教育产品？

背景：
- 目前有 12 个月生活费储蓄
- 已经有一些付费用户，但收入不稳定
- 我担心错过窗口，也担心现金流断掉

请用重大决策会议，并加入红队审查。
```

如果背景不够，life-cabinet 会先进入“决策定义访谈”，帮你把问题问清楚，而不是直接给出看似完整但基础薄弱的建议。

也可以用于轻量问题：

```text
Use $life-cabinet 帮我开一次快速内阁会议：

我最近总是拖延做个人品牌内容，帮我判断卡点在哪里，并给出本周能执行的 3 个动作。
```

HTML 报告默认生成，不需要额外说明：

```text
Use $life-cabinet 分析下面这个重大决策。

议题：
我要不要接受朋友的合伙邀请？

背景：
[补充你的事实、资源、限制、时间期限和担忧]
```

## 会议模式

| 模式 | 适合场景 |
| --- | --- |
| 快速内阁会议 | 日常问题、短期计划、低风险选择、行动卡点 |
| 重大决策会议 | 离职、创业、换城市、合伙、签约、大额投入等高风险事项 |
| 红队审查 | 用户已有计划、商业构想、简历、内容策略或谈判方案 |
| 季度人生董事会复盘 | 月度、季度、年度复盘和下一阶段规划 |
| 一页纸决策备忘录 | 需要简洁、可转发、可归档的决策摘要 |
| HTML 报告 | 需要网页报告、可打印报告或文件版深度分析 |

## 内阁成员

常驻成员包括：

- 内阁秘书长：主持会议、界定问题、整合分歧、形成行动。
- 人生战略顾问：评估长期方向、价值排序和身份成本。
- 商业战略顾问：分析商业模式、定位、增长和资源配置。
- 职业发展顾问：判断机会成本、能力复利和职业资本。
- 财务与风险顾问：识别现金流、下行风险和安全垫问题。
- 法律风险顾问：识别合同、合规、责任和证据风险。
- 温和教练：处理焦虑、拖延、执行阻力和行动拆解。
- 红队审查官：挑战假设、寻找失败路径和盲点。
- 历史视角席：提供受历史人物或公共知识分子思想启发的判断镜头。

也可以按需临时创建专家席，例如产品顾问、技术路线顾问、谈判顾问、关系沟通顾问或健康习惯顾问。

## 用户档案

长期使用时，可以建立用户档案，让内阁团逐渐理解你的职业资产、风险偏好、家庭责任、执行模式和敏感边界。默认位置为：

```text
outputs/life-cabinet/user-profile.md
```

档案遵循以下原则：

- 用户可以跳过任何问题。
- 每条信息需要标注来源、日期、可信度和是否易过期。
- 明确区分“用户陈述的事实”和“AI 推断”。
- 会后只提出“建议写入用户档案”，等待用户确认后再更新。
- 模式 2 中只向子代理传递与角色相关的裁剪信息，不传完整档案。

模板见 [`life-cabinet/assets/user-profile-template.md`](./life-cabinet/assets/user-profile-template.md)。

## HTML 报告

最新版 life-cabinet 默认会为每次咨询生成一个独立报告目录，而不是只在对话框里输出一段总结。HTML 报告使用：

```text
assets/report-template.html
```

报告默认输出到当前工作区：

```text
outputs/life-cabinet/
```

每次咨询会创建独立目录，例如：

```text
outputs/life-cabinet/2026-06-19-1430-career-change/
```

重大决策报告通常会包含：

- `report.html`：最终 HTML 报告。
- `meeting-notes.md`：会议记录中间稿。
- `analysis-brief.md`：秘书长分析备忘录。
- `members/`：成员独立报告目录。

## 目录结构

```text
.
├── README.md
├── README.en.md
├── LICENSE
└── life-cabinet/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   ├── 人生内阁封面.png
    │   ├── 人生内阁封面en.png
    │   ├── report-template.html
    │   └── user-profile-template.md
    └── references/
        ├── meeting-formats.md
        ├── members.md
        ├── prompt-templates.md
        ├── report-output.md
        └── user-profile.md
```

## 定制

- 修改成员定义：编辑 [`life-cabinet/references/members.md`](./life-cabinet/references/members.md)。
- 修改会议流程：编辑 [`life-cabinet/references/meeting-formats.md`](./life-cabinet/references/meeting-formats.md)。
- 修改可复制提示词：编辑 [`life-cabinet/references/prompt-templates.md`](./life-cabinet/references/prompt-templates.md)。
- 修改用户档案规则：编辑 [`life-cabinet/references/user-profile.md`](./life-cabinet/references/user-profile.md)。
- 修改 HTML 输出规范：编辑 [`life-cabinet/references/report-output.md`](./life-cabinet/references/report-output.md) 和 [`life-cabinet/assets/report-template.html`](./life-cabinet/assets/report-template.html)。

## 安全边界

`life-cabinet` 用于结构化思考和决策准备，不替代合格专业人士。

- 不提供法律意见、医疗诊断、税务建议、投资建议或心理治疗。
- 可以帮助识别风险、整理问题清单、准备咨询材料。
- 如果法律、市场、政策、税务规则或近期事实会影响结论，应先核验当前来源。
- 红队审查只批判计划、假设、证据和激励结构，不攻击用户身份或价值。

## 贡献

欢迎围绕以下方向改进：

- 增加新的按需专家席。
- 优化重大决策会议和红队审查模板。
- 改进 HTML 报告的阅读、打印和归档体验。
- 补充更多可复制提示词。
- 加强用户档案的隐私、版本和删除流程。

提交变更时，请保持 `SKILL.md` 精简，把较长的流程、模板和参考材料放入 `references/` 或 `assets/`。

## 许可证

MIT License. See [`LICENSE`](./LICENSE).
