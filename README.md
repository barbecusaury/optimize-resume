# Optimize Resume Skill

中文 | [English](#english)

## 中文

`optimize-resume` 是一个面向 AI Agent 的通用简历优化 Skill。它采用通用 `SKILL.md` 结构，可被支持 Agent Skills 的平台读取和使用，例如 Codex、Claude Code、Gemini CLI，以及其他兼容 `SKILL.md` 技能目录的 agent 环境。

它从抖音知名求职博主“冤种小徐”的写简历教学视频文案中提炼核心方法，并由 AI 延展成可复用的简历优化工作流。

它用于在不修改原简历的前提下，复制一份新的简历文件，只优化文字内容，并在聊天窗口输出一份完整的修改建议。核心思想是让简历更符合 HR 的阅读习惯，把经历写成岗位匹配、结果清晰、数据量化的表达，同时在真实前提下尽可能扩大候选人的呈现边界。

## 适合什么时候用

- 用户发送 `.docx`、PDF、图片或纯文本简历，希望优化简历。
- 用户要求“复制一份新简历，不要改原文件”。
- 用户希望只改文字内容，不改字号、模板、版式。
- 用户希望得到一份优化后的简历，以及一段完整的文字版修改建议。
- 用户需要按岗位 JD 调整经历、项目、技能和个人优势。

## 平台兼容性

这个仓库的核心文件是 `SKILL.md`，它只依赖通用文字指令，不绑定 Codex 专属工具。因此，任何能加载 `SKILL.md` 的 agent 都可以使用这套简历优化流程。

兼容方式：

- Codex：放入 Codex skills 目录后使用 `$optimize-resume` 调用。
- Claude Code：放入 Claude Code skills 目录后按平台的 Skill 调用方式使用。
- Gemini CLI 或其他 agent：放入对应的 skills/agents 目录，确保平台能读取 `SKILL.md` 的 frontmatter 和正文。
- 不支持自动加载 skill 的平台：直接把 `SKILL.md` 内容作为系统/项目指令提供给 agent。

`agents/openai.yaml` 是 Codex/OpenAI 生态的可选 UI 元数据。其他平台不需要读取它，忽略即可；真正的通用逻辑都在 `SKILL.md` 中。

## 主要能力

- 复制原简历并生成优化版，默认不覆盖原文件。
- 保留原有字号、样式和整体排版，只替换或精简文字内容。
- 按 HR 阅读习惯梳理个人信息、教育经历、工作/实习经历、项目经历、个人优势/技能。
- 使用“背景、任务、行动、结果”的四步法重写经历描述。
- 为每条经历添加简洁能力标签，并优先放置岗位相关内容。
- 在真实基础上补充或强化量化结果，例如增长、转化、用户、效率、收入、成本等。
- 输出完整的聊天版修改建议，说明每个模块改了什么、为什么改、还缺什么信息。

## 简历优化原则

### 1. 模板和长度

优先使用白底、上下排列、一页纸简历。避免花哨颜色、图案、封面、封底和长篇介绍。如果用户给的文件不是这种模板，Skill 会优先给出建议，而不是擅自改版。

### 2. 个人信息

个人信息只保留姓名、邮箱、电话和已经提供的正式照片。一般删除或建议删除籍贯、出生日期、薪资、意向岗位、兴趣爱好、星座、MBTI 等弱相关信息。

### 3. 教育经历

教育经历按学校、专业、就读时间写。专业和岗位相关时，可写相关课程；不相关时不强行写。通常只写最高或最有利的真实学历。比如真实拥有专科和本科学历时，优先写本科学历，不必主动暴露较弱路径。

### 4. 工作、实习和项目经历

经历是简历的核心。已毕业写工作经历，在校生写实习经历，没有工作或实习经历时写项目经历。校园学生会、社团、兼职、自媒体等经历，可以在真实前提下整理成项目经历。

推荐写法：

```text
四字标签：针对[背景/问题]，为[任务/目标]，通过[行动/方法/协作]，最终[结果/数据/影响]。
```

示例：

```text
活动策划：针对大促期间用户活跃度低的问题，为提升用户活跃度，策划打卡、引流、裂变等互动方案并协调设计落地，最终带动活动参与人数突破20万人。
```

### 5. 个人优势和技能

避免空话，例如“积极乐观”“学习能力强”“沟通能力强”。优先写证书、奖项、竞赛、工作成绩和可验证技能。

对于 Office、Excel 数据透视表、PPT、PS、PR、剪映等容易验证和可短期补齐的技能，可以在真实边界内写基础水平，例如“熟悉”“掌握基础”“可完成基础操作”。同时应在修改建议中提醒用户投递或面试前补齐练习。

## 真实性边界

这个 Skill 不是伪造经历工具。它允许最大化真实表达，但不允许编造事实。

可以做：

- 真实拥有本科时，优先写本科。
- 选择对自己更有利的真实数据和表达角度。
- 把弱描述改成结果导向表达。
- 对可短期补齐的基础技能使用保守表述。

不能做：

- 编造学历、学校层级、公司、岗位、日期、证书、奖项、项目或照片。
- 把不会的复杂技能写成精通。
- 写无法解释、无法验证、无法在面试前补齐的能力。
- 虚构量化数据。

## 安装

### Codex

```powershell
git clone https://github.com/barbecusaury/optimize-resume.git D:\GithubProject\codex-home\skills\optimize-resume
```

如果你已经有该目录，可以进入目录后更新：

```powershell
git pull
```

### 其他 Agent 平台

把仓库克隆到该平台约定的 skills 目录，或复制整个 `optimize-resume` 文件夹：

```bash
git clone https://github.com/barbecusaury/optimize-resume.git <your-agent-skills-dir>/optimize-resume
```

如果平台不支持技能目录，把 `SKILL.md` 的内容作为该 agent 的项目说明、系统说明或长期指令使用。

## 使用示例

```text
Use $optimize-resume 优化这份简历。要求复制一份新简历，不修改原文件，只改文字内容，不改字号，并输出完整修改建议。
```

也可以补充目标岗位：

```text
Use $optimize-resume 按新媒体运营岗位优化我的简历，突出活动策划、内容运营、数据分析和增长结果。
```

## 输出效果

使用后应得到：

- 一份新的优化版简历文件，原简历保持不变。
- 一段聊天窗口内的完整修改建议。
- 对缺失数据、缺失证据、需要补学技能的提醒。

---

## English

`optimize-resume` is a universal resume optimization skill for AI agents. It uses the common `SKILL.md` structure, so platforms that support Agent Skills can read and use it, including Codex, Claude Code, Gemini CLI, and other agent environments compatible with `SKILL.md` skill folders.

It distills the core method from the resume-writing tutorial transcript of the well-known Douyin job-search creator "冤种小徐", then extends it with AI into a reusable resume optimization workflow.

It creates a revised copy of the user's resume, edits wording only, preserves the original file, and returns complete revision advice in the chat. The core idea is to make the resume easier for HR to scan, rewrite experience around job fit and measurable outcomes, and present the candidate's real background in the strongest honest way.

## When to Use

- A user provides a `.docx`, PDF, image, or plain-text resume and asks for resume optimization.
- A user wants a new resume copy without modifying the original file.
- A user wants wording improvements only, without changing font size, layout, or template.
- A user wants both an optimized resume and a complete text explanation of the changes.
- A user wants to tailor experience, projects, skills, or strengths to a target job description.

## Platform Compatibility

The core file in this repository is `SKILL.md`. It contains tool-agnostic text instructions and does not depend on Codex-only tools, so any agent that can load `SKILL.md` can use the workflow.

Compatibility options:

- Codex: place this repository in the Codex skills directory and invoke it as `$optimize-resume`.
- Claude Code: place it in the Claude Code skills directory and invoke it using that platform's Skill mechanism.
- Gemini CLI or other agents: place it in the relevant skills/agents directory, as long as the platform can read `SKILL.md` frontmatter and body.
- Platforms without automatic skill loading: paste `SKILL.md` into the agent's system, project, or long-term instructions.

`agents/openai.yaml` is optional UI metadata for the Codex/OpenAI ecosystem. Other platforms can ignore it; the portable skill logic lives in `SKILL.md`.

## Key Capabilities

- Copy the source resume and generate a separate optimized version.
- Preserve existing font size, style, and layout wherever possible.
- Improve personal information, education, work/internship experience, project experience, and strengths/skills.
- Rewrite bullets with the Background, Task, Action, Result structure.
- Add concise capability labels to experience bullets.
- Strengthen quantified outcomes using truthful data.
- Return complete revision advice in chat, including missing information and risk notes.

## Resume Rules

### 1. Template and Length

Prefer a white-background, top-to-bottom, one-page resume. Avoid colorful decoration, covers, back covers, and long introductions. If the user's current file does not match this format, the skill should explain the issue instead of silently redesigning the file.

### 2. Personal Information

Keep only name, email, phone number, and a formal photo if already provided. Remove or recommend removing weakly relevant information such as hometown, birth date, salary expectation, target role, hobbies, zodiac sign, MBTI, and similar filler.

### 3. Education

Write school, major, and study dates. Add relevant coursework only when it supports the target role. Usually show the highest or most favorable true degree. For example, if the candidate truthfully has both associate and bachelor education, show the bachelor degree first and do not expose the weaker path unless requested.

### 4. Work, Internship, and Project Experience

Experience is the core of the resume. Graduates use work experience, students use internship experience, and candidates without work or internship experience use project experience. Campus organizations, clubs, part-time work, and self-media work may be reframed as project experience when truthful.

Recommended bullet structure:

```text
Label: For [background/problem], to [task/goal], used [action/method/collaboration], resulting in [outcome/data/impact].
```

Example:

```text
Campaign Planning: For low user activity during a major promotion, designed check-in, traffic-driving, and referral interaction plans, coordinated design execution, and helped the campaign reach over 200,000 participants.
```

### 5. Strengths and Skills

Avoid empty claims such as "optimistic," "fast learner," or "strong communication skills" unless supported by evidence. Prefer certificates, awards, competitions, work results, and concrete skills.

For easy-to-verify and quickly learnable workplace skills such as Office, Excel pivot tables, PowerPoint, Photoshop, Premiere/PR, or Jianying/CapCut, the skill may use conservative levels such as "familiar with," "basic proficiency," or "can complete basic operations." It should also remind the user to practice before interviews or delivery.

## Honesty Boundary

This skill is not for fabricating experience. It may maximize honest presentation, but it must not invent facts.

Allowed:

- Show a real bachelor degree when the candidate also has an associate degree.
- Choose favorable truthful metrics and phrasing.
- Turn weak duty descriptions into outcome-focused bullets.
- Use conservative wording for basic skills that can be quickly learned or verified.

Not allowed:

- Invent education, school labels, companies, roles, dates, certificates, awards, projects, or photos.
- Claim advanced proficiency in skills the user cannot support.
- Add abilities that cannot be explained, verified, or learned before the interview.
- Fabricate quantified results.

## Installation

### Codex

```powershell
git clone https://github.com/barbecusaury/optimize-resume.git D:\GithubProject\codex-home\skills\optimize-resume
```

If the directory already exists, update it with:

```powershell
git pull
```

### Other Agent Platforms

Clone the repository into the skills directory expected by your agent platform, or copy the whole `optimize-resume` folder:

```bash
git clone https://github.com/barbecusaury/optimize-resume.git <your-agent-skills-dir>/optimize-resume
```

If your platform does not support skill directories, use the contents of `SKILL.md` as system, project, or persistent instructions for the agent.

## Example Prompts

```text
Use $optimize-resume to optimize this resume. Copy it first, do not modify the original file, edit wording only, preserve font size, and return complete revision advice.
```

With a target role:

```text
Use $optimize-resume to tailor my resume for a new media operations role. Emphasize campaign planning, content operations, data analysis, and growth outcomes.
```

## Expected Output

The skill should produce:

- A separate optimized resume file while preserving the original.
- Complete revision advice in the chat.
- Notes about missing metrics, missing evidence, and skills the user should practice before using the resume.
