---
name: optimize-resume
description: Use when a user provides resume text or a resume file and asks an AI agent to optimize, rewrite, polish, tailor for a job, create a revised resume copy, or return resume revision advice while preserving the original.
---

# Optimize Resume

## Overview

Create a revised resume from the user's existing resume while preserving the original file. Optimize wording for HR scanning, role fit, evidence, and quantified results; output both the revised resume artifact and a complete text version of the revision advice in chat.

## Non-Negotiable Constraints

1. Preserve the original resume. Never edit the source file in place.
2. If the user provides a file, copy it first and edit only the copy. Use a clear name such as `<original-name>-optimized.docx`.
3. Modify text content only. Do not change font size, page size, margins, colors, decorations, or template structure unless the user explicitly asks.
4. Do not fabricate facts. Never invent education level, school labels, dates, companies, roles, certificates, awards, metrics, salary, or photos.
5. Use maximum honest framing. Present the user's real background in the most favorable truthful way: omit weaker details when not required, choose stronger true labels, use favorable true metrics, and expand ability boundaries only where the user can realistically learn or verify the skill before interview or work delivery.
6. Return a chat summary that includes: revised file path or revised text, complete revision advice, unresolved missing information, and what was intentionally not changed.

## Artifact Workflow

1. Identify input type:
   - `.docx`: make a copy, extract text, edit paragraphs/table cells in the copy while preserving existing styles and font sizes.
   - `.pdf` or image: extract readable text for advice. If the file is not directly editable, create a text/DOCX revision only when reasonable and state that the original visual layout could not be edited safely.
   - Plain text: return a revised text resume in chat; create a file only if requested.
2. Identify target context:
   - Use the user's stated target role, job description, industry, or seniority.
   - If missing, infer cautiously from the resume and mark assumptions in the advice.
3. Edit by replacing or trimming wording in existing sections. For `.docx`, avoid rebuilding the whole document unless the file is unusable.
4. Verify the original file remains unchanged and the revised copy exists.
5. In chat, output concise but complete advice grouped by resume section.

## Resume Structure Rules From the Transcript

Use these rules as the optimization rubric. Apply them within the non-negotiable constraints above.

| Area | Rule |
| --- | --- |
| Template | Prefer a white-background, top-to-bottom resume layout that matches HR reading habits. Avoid colorful graphics, decorative patterns, covers, back covers, and long introductory pages. |
| Length | Keep the resume to one page when possible. If font size cannot be changed, reduce irrelevant text and tighten wording instead of shrinking text. |
| Section order | A strong resume should normally contain five parts from top to bottom: personal information, education, work/internship experience, project experience, and personal strengths/skills. |
| Personal information | Keep only name, email, phone, and a neat formal photo if already present or provided. Remove or advise removing irrelevant items such as hometown/native place, birth date, salary expectation, target role, interests, zodiac sign, MBTI, and similar filler. |
| Education | Write school, major, and study dates from left to right. Include relevant coursework only when the major matches the target role. Usually keep only the highest or most favorable true degree. If the user has both associate and bachelor education, write the bachelor degree and omit the weaker associate path unless the user asks to show full history. If the school is truthfully 985/211/Double First-Class, mark it in parentheses after the school name. |
| Weak education | If education is not competitive for the role, advise placing it lower in the resume. Do not reorder the file layout automatically if only text edits are allowed. |
| Work/internship/project experience | Treat this as the resume's core. Graduates use work experience; current students use internships; users without work/internship experience use projects. Company work must be work actually done in a company. Campus work, student union, clubs, part-time work, and self-media can be reframed as project experience when truthful. |
| Experience heading | Use company name + role + dates for work/internship; use project name + role + dates for projects. |
| Bullet count | Under each experience, write 3-5 concise bullets. |
| Bullet opening | Start each bullet with a condensed four-character capability label, then a description. If styling edits are allowed, bold the label; otherwise keep the label as plain text and mention bolding in advice. |
| Bullet method | Write each description with the four-step rule: background, task, action, result. The sentence should show what problem existed, what goal was set, what the user did, and what measurable result followed. |
| Job matching | Choose bullet topics that match the target job description. If the JD requires copywriting, include truthful copywriting work; if it requires data analysis, include truthful data analysis work. |
| Quantification | Add data wherever truthful: growth, conversion, revenue, traffic, users, cost reduction, efficiency, delivery time, ranking, completion rate, or volume. |
| Favorable framing | Select favorable truthful metrics. Example: from 100 to 300 followers can be written as "reached 3x the original follower base" or "net growth of 200%"; avoid mathematically false wording. |
| Personal strengths | Do not write empty claims such as "optimistic," "strong learning ability," or "strong communication skills" without proof. Use certificates, awards, competitions, work results, and concrete skills as evidence. |
| Skills | If there are few achievements, list easy-to-verify workplace skills such as Office, Excel pivot tables, PPT document/deck building, Photoshop/image processing, and video editing tools such as Premiere/PR or Jianying. For simple skills near the user's ability boundary, the resume may write a basic truthful level such as "熟悉/掌握基础/可完成基础操作," but the user should be told to learn and practice them before interview or delivery. Do not write advanced proficiency, certificates, or specialized capabilities the user cannot realistically support. |

## Experience Bullet Formula

Use this shape for work and project bullets:

```text
四字标签：针对[背景/问题]，为[任务/目标]，通过[行动/方法/协作]，最终[结果/数据/影响]。
```

Example adapted from the transcript:

```text
活动策划：针对大促期间用户活跃度低的问题，为提升用户活跃度，策划打卡、引流、裂变等互动方案并协调设计落地，最终带动活动参与人数突破20万人。
```

Prefer strong verbs such as planned, coordinated, analyzed, optimized, built, delivered, converted, increased, reduced, and launched. Replace vague verbs like participated in, responsible for, assisted with, and helped with unless the user truly only assisted.

## Editing Guidance

- Delete or rewrite filler before adding new text.
- Keep one bullet to one main contribution.
- Put the most role-relevant and quantified bullets first.
- Convert duties into outcomes. Bad: "Responsible for account operation." Better: "内容运营：围绕新品推广目标，制定选题日历并复盘互动数据，推动账号月均阅读量提升32%。"
- If evidence is missing, write a conservative version and add a missing-data note in chat.
- If the current template is colorful, multi-column, longer than one page, or has a cover, explain the issue in the advice instead of silently redesigning the file.
- For education and skill claims, keep the transcript's intent of expanding the user's presentation boundary: write the strongest true education path, choose simple learnable skills when appropriate, and avoid exposing unnecessary weaknesses. The boundary is "can truthfully explain or quickly补齐," not "already perfect."
- When adding near-boundary skills, include a note in the chat advice telling the user exactly what to learn or practice before using the resume.

## Chat Output Format

After editing, respond with:

```markdown
已生成优化版简历：[filename/path]

修改建议：
1. 个人信息：...
2. 教育经历：...
3. 工作/实习经历：...
4. 项目经历：...
5. 个人优势/技能：...
6. 格式与风险：...

仍需补充：
- ...
```

If no file could be edited, replace the first line with the revised resume text and clearly state why an editable copy was not produced.
