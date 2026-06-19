# 人生内阁团 Life Cabinet

<p align="center">
  <img src="./life-cabinet/assets/人生内阁封面.png" alt="人生内阁团封面" width="260" />
</p>

> 召集一个 AI 人生内阁团，为职业、事业、人生规划、财富风险、法律风险、心理状态和执行行动提供结构化讨论。

`life-cabinet` 是一个中文 agent skill，适用于 Codex、Claude Code、Gemini CLI、Cursor 等支持技能、规则或上下文扩展的主流智能体工具。它把一次咨询组织成“内阁会议”：先澄清问题，再选择合适的顾问角色，形成独立意见、红队审查、交叉质询和秘书长综合结论。

它适合用于：

- 职业选择：跳槽、转行、晋升、离职、个人品牌。
- 事业判断：创业、副业、商业模式、合伙、内容商业化。
- 重大人生决策：换城市、长期规划、家庭责任、生活方式取舍。
- 风险审查：合同、现金流、投资风险、执行阻力、方案盲点。
- 阶段复盘：月度、季度、年度人生董事会复盘。

## 特性

- **少召集、强区分、重综合**：默认只选择 3-8 位真正相关的成员，避免所有角色轮流表演。
- **两种执行模式**：默认使用同一上下文中的深度会议；明确要求时可升级为真实 Subagent 模式。
- **成员独立报告**：重大决策、深度报告和 HTML 报告会先生成成员报告，再由秘书长整合。
- **红队审查**：对高风险、不可逆或成本很高的决策，强制加入红队审查官。
- **用户档案系统**：支持长期用户档案，但要求区分事实与 AI 推断，且不静默更新。
- **HTML 报告模板**：可生成适合阅读、打印和归档的网页报告。
- **安全边界清晰**：法律、医疗、税务、投资和心理健康议题只做风险识别与咨询准备。

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

也可以用于轻量问题：

```text
Use $life-cabinet 帮我开一次快速内阁会议：

我最近总是拖延做个人品牌内容，帮我判断卡点在哪里，并给出本周能执行的 3 个动作。
```

生成 HTML 报告：

```text
Use $life-cabinet 分析下面这个重大决策，并额外生成 HTML 报告。

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

长期使用时，可以建立用户档案，默认位置为：

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

当用户要求生成网页报告、可打印报告或文件版报告时，Skill 会使用：

```text
assets/report-template.html
```

报告默认输出到当前工作区：

```text
outputs/life-cabinet/
```

重大决策报告通常会包含：

- `*-report.html`：最终 HTML 报告。
- `*-meeting-notes.md`：会议记录中间稿。
- `*-analysis-brief.md`：秘书长分析备忘录。
- `*-members/`：成员独立报告目录。

## 目录结构

```text
.
├── README.md
├── LICENSE
└── life-cabinet/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   ├── 人生内阁封面.png
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
