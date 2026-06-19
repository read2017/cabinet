# HTML 报告输出

## 使用场景

当用户要求“输出报告”“生成 HTML 报告”“做成网页报告”“除了对话框再给我一个文件”“可打印版本”或类似需求时，除在对话框内给出结论外，还应生成一个 HTML 报告文件。

模式 2 真实 Subagent 模式默认触发本流程；不需要用户额外要求 HTML。只要本次执行模式为模式 2，最终交付就必须包含 HTML 报告、会议记录中间稿、秘书长分析备忘录和成员报告目录。

每次咨询必须在 `outputs/life-cabinet/` 下创建一个独立咨询目录；本次咨询生成的 HTML、会议记录、分析备忘录和成员报告都放进这个目录，避免长期使用后文件互相混淆。

默认模板：

```text
life-cabinet/assets/report-template.html
```

## 输出位置

在当前工作区创建报告文件。每次咨询先创建独立目录，目录名使用 `YYYY-MM-DD-HHMM-brief-topic/`：

```text
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/
```

重大决策 HTML 报告必须在该目录内同时创建三个文件：

```text
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/report.html
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/meeting-notes.md
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/analysis-brief.md
```

重大决策、深度报告或模式 2 真实 Subagent 报告还必须在该目录内创建成员报告目录：

```text
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/members/
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/members/finance-advisor.md
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/members/legal-risk-advisor.md
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/members/relationship-coach.md
outputs/life-cabinet/YYYY-MM-DD-HHMM-brief-topic/members/red-team.md
```

如果当前工作区没有 `outputs/life-cabinet/`，先创建目录。目录名和文件名使用小写英文、数字和连字符；中文议题可转成简短英文 slug，例如：

- `2026-06-18-1430-career-change/`
- `2026-06-18-1515-startup-decision/`
- `2026-06-18-1600-quarterly-review/`

`outputs/life-cabinet/user-profile.md` 是长期用户档案，可以继续放在根目录；它不属于某一次咨询目录。

## 生成流程

1. 正常运行人生内阁会议，并在对话框输出简洁结论。
2. 先创建本次咨询目录和 `members/` 子目录。
3. 先生成成员独立报告。每个关键成员单独保存一份 `.md` 到本次咨询目录的 `members/` 子目录；成员报告是用户等待过程中的可读产物，也是秘书长最终综合的证据来源。
4. 每份成员报告完成后，在对话框用 1-3 句话提示该成员的一句话建议和文件路径。不要等全部完成后才告知。
5. 检查成员报告是否齐全。重大决策至少应有 4 份成员报告，且必须包含红队报告；如缺失，先补派、补写或明确标注缺失原因，不得伪装成已参与。
6. 再生成会议记录中间稿 `meeting-notes.md`。会议记录是原始材料，要保留成员报告摘要、角色立场、理由链、质询、回应、分歧和秘书长阶段总结。
7. 再生成秘书长分析备忘录 `analysis-brief.md`。分析备忘录把成员报告和会议记录整理成专业报告逻辑，包括执行摘要、决策框架、因果链、反事实、场景推演、阈值和路线图。
8. 读取 `assets/report-template.html`。
9. 把分析备忘录、会议记录和成员报告索引转换为 HTML 片段，替换模板占位符。
10. 将完整 HTML 写入本次咨询目录的 `report.html`。HTML 前半部分展示专业分析报告，最后展示会议纪要、成员报告索引和完整会议记录。
11. 最后在回复中给出本次咨询目录、HTML、会议记录中间稿、分析备忘录和成员报告目录路径。

## 成员报告文件要求

每份成员报告必须是 Markdown 文件，文件名使用角色英文 slug。建议角色映射：

| 角色 | 文件名 |
| --- | --- |
| 人生战略顾问 | `life-strategy-advisor.md` |
| 商业战略顾问 | `business-strategy-advisor.md` |
| 职业发展顾问 | `career-advisor.md` |
| 财务与风险顾问 | `finance-risk-advisor.md` |
| 法律风险顾问 | `legal-risk-advisor.md` |
| 关系沟通顾问 | `relationship-communication-advisor.md` |
| 温和教练 | `gentle-coach.md` |
| 红队审查官 | `red-team-reviewer.md` |

每份成员报告必须包含：

- 标题和生成日期；
- 角色边界；
- 一句话建议；
- 给用户的摘要；
- 判断标准；
- 至少 3 条“如果 A，则 B，因此 C”的理由链；
- 关键风险和失败路径；
- 反事实分析；
- 决策阈值表；
- 需要补充或核验的信息；
- 未来 30 天最小行动；
- 给秘书长的备忘，包括可能冲突的成员、必须保留的风险和置信度。

模式 2 真实 Subagent 中，成员报告正文应来自对应子代理输出。秘书长可以做格式整理、标题补齐和轻微错字修正，但不能改写成员的核心立场。

## 中间稿文件要求

`meeting-notes.md` 必须包含：

- 标题、生成日期、会议模式和执行模式；
- 本次使用的用户画像假设；
- 决策问题重写、备选方案和关键变量；
- 参会成员与角色边界；
- 成员独立报告索引：列出每份成员报告路径和一句话建议；
- 第一轮独立意见摘要：每个关键角色至少包含立场、三条理由链、最大风险、需要验证的信息；
- 关键分歧；
- 第二轮交叉质询：至少 3 组质询和回应；
- 红队挑战与回应；
- 立场变化记录；
- 秘书长阶段性总结和最终冲突处理；
- 建议写入用户档案的事项，如有。

`analysis-brief.md` 必须包含：

- 执行摘要；
- 决策问题和用户画像假设；
- 备选方案与判断标准；
- 核心结论与成立条件；
- 结构化论证：因果链、反事实、场景推演；
- 红队预演与风险登记；
- 决策阈值和行动路线图；
- 未解决问题和专业咨询提示。

## 占位符

| 占位符 | 内容 |
| --- | --- |
| `{{REPORT_TITLE}}` | 报告标题，例如“离职创业重大决策报告” |
| `{{REPORT_SUBTITLE}}` | 一句话副标题，说明议题和目的 |
| `{{MEETING_FORMAT}}` | 快速内阁会议、重大决策会议、红队审查或季度人生董事会复盘 |
| `{{GENERATED_AT}}` | 生成日期和时间 |
| `{{DECISION_STATUS}}` | 建议推进、建议暂缓、需要补充信息、建议修改后推进等 |
| `{{EXECUTIVE_SUMMARY_HTML}}` | 执行摘要：建议、信心等级、成立条件 |
| `{{SITUATION_HTML}}` | 问题与背景，使用 `<p>`、`<ul>` 或 `<table>` |
| `{{USER_PROFILE_ASSUMPTIONS_HTML}}` | 本次使用的用户画像假设和需要确认的信息 |
| `{{OPTIONS_FRAMEWORK_HTML}}` | 备选方案、判断标准、权重和不可接受代价 |
| `{{PARTICIPANTS_HTML}}` | 参会成员卡片，每个成员使用 `.role` |
| `{{DECISION_LOGIC_HTML}}` | 核心判断、决策逻辑树、关键因果链和量化阈值 |
| `{{DISCUSSION_HTML}}` | 深度论证内容，优先围绕主问题展开，不机械平均分配给每个角色 |
| `{{SCENARIO_ANALYSIS_HTML}}` | 乐观、基准、悲观情景和反事实推演 |
| `{{RED_TEAM_HTML}}` | 红队审查内容；如不适用，写“本次会议未启用红队审查。” |
| `{{RISK_REGISTER_HTML}}` | 风险表；无风险表时给出简短说明 |
| `{{ROADMAP_HTML}}` | 阶段路线图，例如 30 天、90 天、6 个月 |
| `{{NEXT_ACTIONS_HTML}}` | 下一步行动，优先使用 `<ol>` |
| `{{OPEN_QUESTIONS_HTML}}` | 未解决问题，优先使用 `<ul>` |
| `{{PROFESSIONAL_FLAGS_HTML}}` | 法律、医疗、税务、投资、心理健康等专业咨询提示 |
| `{{ARTIFACT_LINKS_HTML}}` | 指向会议记录中间稿和分析备忘录的本地链接 |
| `{{MEETING_SUMMARY_HTML}}` | 会议纪要：成员报告索引、关键分歧、采纳观点、保留争议 |
| `{{FULL_MEETING_RECORD_HTML}}` | 完整会议记录，由 `meeting-notes.md` 转成 HTML |
| `{{FOOTER_NOTE}}` | 固定边界说明 |

## 参会成员 HTML 片段

```html
<div class="role">
  <strong>内阁秘书长</strong>
  <p>主持会议，整合分歧，形成最终建议。</p>
</div>
```

## 风险登记表 HTML 片段

```html
<table>
  <thead>
    <tr>
      <th>风险</th>
      <th>概率</th>
      <th>影响</th>
      <th>缓解动作</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>现金流不足</td>
      <td>中</td>
      <td>高</td>
      <td>先建立 6-12 个月安全垫。</td>
    </tr>
  </tbody>
</table>
```

## HTML 内容规则

- 模板是完整 HTML 文件，不要引入外部 CSS、JS、字体或图片。
- 模板包含左上角目录按钮和侧边目录，保留内联 CSS/JS；不要引入外部库。
- 用户提供的文本进入 HTML 前要避免破坏结构；必要时转义 `<`、`>`、`&`。
- 不要把 Markdown 直接塞进模板；先转成 `<p>`、`<ul>`、`<ol>`、`<table>` 等 HTML。
- 深度报告不能只写成员短评；必须包含因果链、反事实、量化阈值、例证或情境推演、红队预演和阶段路线图。
- 模式 1 报告要写清模拟会议过程，且成员报告和会议记录中间稿必须落盘；模式 2 报告要区分子代理成员报告、交叉质询记录和秘书长综合结论。
- HTML 正文先展示专业分析报告，再展示会议纪要和完整会议记录；不要把完整会议记录放在报告开头。
- HTML 的中间稿附件区应链接成员报告目录或关键成员报告文件；如果链接相对路径，必须确保从 HTML 文件位置可打开。
- 如使用用户档案，应在“问题与背景”或“核心判断与决策逻辑”中说明本次使用的档案假设和需要更新的信息；不要把完整用户档案写入 HTML 报告。
- 会后档案更新建议放在对话框输出即可，除非用户明确要求写进报告。
- 报告应可直接用浏览器打开，也应适合打印为 PDF。
- 对话框输出保持简洁，不要把完整 HTML 源码贴回对话框，除非用户明确要求。

## 固定页脚文案

默认使用：

```text
本报告由 AI 人生内阁团生成，用于结构化思考和决策准备。涉及法律、医疗、税务、投资或心理健康事项时，请咨询合格专业人士。
```
