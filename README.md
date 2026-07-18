# Big Project Skill

面向大型软件项目的 Codex/Agent Skill 集合，用 GitHub Issues、Feature Spec 与当前功能总览形成职责清晰、可追踪的需求与文档闭环。

## 包含的 Skills

| Skill | 职责 | 适用场景 |
| --- | --- | --- |
| [`big-project-issue-manager`](big-project-issue-manager/SKILL.md) | 管理 GitHub Issue 的分类、拆分、关联、迁移与关闭检查 | 维护 Idea、Epic、Feature、Bug、文档和维护事项的协作状态 |
| [`big-project-spec`](big-project-spec/SKILL.md) | 维护 Feature 的 Spec、Plan、Tasks、Checklist 等设计与实施产物 | 规划、澄清、分析、实现或收敛 `docs/specs/<issue-number>-<feature-slug>/` |
| [`big-project-overview-maintainer`](big-project-overview-maintainer/SKILL.md) | 维护已落地功能的权威总览 | 初始化或增量更新 `docs/overview/`，同步代码已经证明的当前行为 |

## 协作模型

三类信息分别保存在各自的权威来源中：

```text
GitHub Issues
  └─ 未完成工作的协作状态、类型、依赖与父子关系

docs/specs/<issue-number>-<feature-slug>/
  └─ 单个 Feature 的需求、设计、任务与验收

docs/overview/
  └─ 已经实现并可由代码、配置或测试证明的当前功能事实
```

推荐流程：

1. 使用 `big-project-issue-manager` 创建或整理需求，并确认对应的 `type:*` 标签。
2. 对已采纳的 Feature 使用 `big-project-spec` 建立 Spec、Plan、Tasks 与质量门。
3. 完成实现和验收后，使用 `big-project-overview-maintainer` 将已落地行为同步到 `docs/overview/`。
4. 完成 Documentation Impact 检查后，再关闭对应 Issue。

## 安装

将需要的 Skill 目录复制到目标项目的 `.agents/skills/`：

```bash
git clone https://github.com/JLU-ICCMS-MaYuan/Big-Project-Skill.git

cp -R Big-Project-Skill/big-project-issue-manager <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-spec <project>/.agents/skills/
cp -R Big-Project-Skill/big-project-overview-maintainer <project>/.agents/skills/
```

也可以将这些目录放入 Agent 支持的个人 Skill 目录。具体发现路径以所使用的 Agent 文档为准。

## 使用要求

- 执行前先读取目标仓库的 `AGENTS.md`；仓库规则优先于 Skill 默认规则。
- Issue number 同时作为 Feature Spec 目录编号，避免多人并行时发生编号冲突。
- Overview 只记录已经落地的事实，不记录尚未实现的计划或假设。
- 各 Skill 的完整触发条件、边界和工作流以对应目录中的 `SKILL.md` 为准。
