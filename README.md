# Big Project Skill

面向大型软件项目的 Codex/Agent Skill 集合，用前期总体规划、GitHub Issues、Feature Spec 与当前功能总览形成职责清晰、可追踪的需求与文档闭环。

## 包含的 Skills

| Skill | 职责 | 适用场景 |
| --- | --- | --- |
| [`big-project-planer`](big-project-planer/SKILL.md) | 通过多轮设计树访谈，将初步想法整理为前期总体规划 | 挖掘潜在需求，明确范围、能力地图、架构方向、风险与阶段路线，并写入 `docs/plan/` |
| [`big-project-contractor`](big-project-contractor/SKILL.md) | 将已确认总体规划完整拆成 Feature 与 Spec，通过全局文档门后依次实现 | 新项目或大型版本需要先得到完整需求蓝图，再由 AI 按依赖连续交付 |
| [`big-project-issue-manager`](big-project-issue-manager/SKILL.md) | 管理 GitHub Issue 的分类、拆分、关联、迁移与关闭检查 | 维护 Idea、Epic、Feature、Bug、文档和维护事项的协作状态 |
| [`big-project-spec-runner`](big-project-spec-runner/SKILL.md) | 维护 Feature 的 Spec、Plan、Tasks、Checklist 等设计与实施产物 | 规划、澄清、分析、实现或收敛 `docs/specs/<issue-number>-<feature-slug>/` |
| [`big-project-overview-maintainer`](big-project-overview-maintainer/SKILL.md) | 维护已落地功能的权威总览 | 初始化或增量更新 `docs/overview/`，同步代码已经证明的当前行为 |
| [`big-project-translator`](big-project-translator/SKILL.md) | 用大白话和具体例子解释复杂内容 | 解释代码、架构、方案、报错或文档，减少专业术语和抽象表达 |

## 协作模型

四类信息分别保存在各自的权威来源中：

```text
docs/plan/<plan-slug>.md
  └─ 前期总体目标、能力地图、架构方向、跨功能约束、风险与阶段路线

GitHub Issues
  └─ 未完成工作的协作状态、类型、依赖与父子关系

docs/specs/<issue-number>-<feature-slug>/
  └─ 单个 Feature 的需求、设计、任务与验收

docs/overview/
  └─ 已经实现并可由代码、配置或测试证明的当前功能事实
```

新项目或大型版本推荐流程：

1. 对尚未成形的大型项目构想，使用 `big-project-planer` 完成总体规划和阶段边界。
2. 使用 `big-project-contractor` 将规划完整拆成 Epic、Feature 和全部 Spec；所有文档通过全局质量门后，再按依赖顺序逐项实现。
3. 每个 Feature 实现和验收后，使用 `big-project-overview-maintainer` 将已落地行为同步到 `docs/overview/`，完成 Documentation Impact 后关闭 Issue。
4. 项目进入常规维护期后，小需求和 Bug 使用 `big-project-issue-manager` 与 `big-project-spec-runner` 单独处理，不再重跑 Contractor。

## 安装

将需要的 Skill 目录复制到目标项目的 `.agents/skills/`：

```bash
git clone https://github.com/JLU-ICCMS-MaYuan/Big-Project-Skill.git

cp -R Big-Project-Skill/big-project-planer <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-contractor <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-issue-manager <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-spec-runner <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-overview-maintainer <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-translator <project>/.agents/skills/
```

也可以将这些目录放入 Agent 支持的个人 Skill 目录。具体发现路径以所使用的 Agent 文档为准。

## 使用要求

- 执行前先读取目标仓库的 `AGENTS.md`；仓库规则优先于 Skill 默认规则。
- 总体规划只记录前期目标、方向和阶段边界，不替代 Feature Spec 或当前功能 Overview。
- Contractor 只用于新项目或大型版本的初始完整交付；全部 Spec 文档通过质量门前不得开始实现。
- Issue number 同时作为 Feature Spec 目录编号，避免多人并行时发生编号冲突。
- Overview 只记录已经落地的事实，不记录尚未实现的计划或假设。
- 各 Skill 的完整触发条件、边界和工作流以对应目录中的 `SKILL.md` 为准。
