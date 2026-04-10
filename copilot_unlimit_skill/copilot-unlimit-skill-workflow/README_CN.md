# kokomoon-workflow

一个面向 AI 智能体的交互式工作流 Skill，强制执行"设计-审核-执行"循环，并在每个阶段要求用户确认。

## 功能说明

该 Skill 确保 AI 智能体遵循以下工作流程：

1. **分析** — 深入分析用户的需求，研究相关代码和上下文
2. **设计** — 产出详细的方案设计说明和结构化的 todolist
3. **确认** — 通过交互式询问窗口向用户确认方案
4. **执行** — 仅在用户确认后开始执行任务
5. **复核** — 执行完成后再次向用户确认结果

**核心强制约束**：智能体**不得**在未获得用户明确同意的情况下结束对话。

## 安装方法

### VS Code（GitHub Copilot）

将 `kokomoon-workflow/` 目录复制到以下任一路径：
- `.github/skills/`（项目级，仅对当前项目生效）
- `~/.copilot/skills/`（用户级，全局生效）

### Claude Code

复制到 `.claude/skills/` 目录，或通过插件市场安装。

### 其他 Agent Skills 兼容客户端

放到客户端扫描的 skills 目录中，遵循 [Agent Skills 规范](https://agentskills.io/specification)。

## 使用方式

Skill 会在智能体检测到多步骤任务时自动激活。也可以通过斜杠命令手动调用：

```
/kokomoon-workflow 分析音频信号链路并修复输出问题
```

## 规范合规性

本 Skill 遵循 [Agent Skills 规范](https://agentskills.io/specification)：
- YAML frontmatter 包含必需的 `name` 和 `description` 字段
- 可选字段：`license`、`compatibility`、`metadata`
- Markdown 正文包含结构化的工作流指令
- 文件长度友好，符合渐进式披露原则（< 500 行）

## 目录结构

```
kokomoon-workflow/
├── SKILL.md      ← Skill 定义文件（元数据 + 行为指令）
├── LICENSE        ← Apache-2.0 开源许可证
├── README.md      ← 英文说明文档
└── README_CN.md   ← 中文说明文档
```

## 许可证

Apache-2.0，详见 [LICENSE](./LICENSE)。
