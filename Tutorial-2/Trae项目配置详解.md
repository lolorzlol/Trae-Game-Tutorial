# Trae 项目配置详解

`.trae/` 目录下放的是项目配置，这篇文章把结构捋清楚，方便你复制到自己的项目里用。

---

## 架构总览

```
┌─────────────────────────────────────────────────────────────────────────┐
│                            项目根目录                                     │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   AGENTS.md                        ┌─────────────────────────┐          │
│   (项目级指令)                      │     Unity Editor        │          │
│   ├─ 工作流程定义                   │   (localhost:8080)      │          │
│   ├─ 代码规范                       └───────────┬─────────────┘          │
│   └─ 偏好设置                                   │ MCP                    │
│                                                 ▼                        │
│   .trae/                          ┌─────────────────────────┐          │
│   ├─ mcp.json ──────────────────► │     unityMCP Server     │          │
│   │  (MCP服务器配置)               │                         │          │
│   │                               └─────────────────────────┘          │
│   ├─ agents/                                                            │
│   │  └─ code-reviewer.md         ┌─────────────────────────┐          │
│   │     (代码审查Agent)           │        Trae IDE          │          │
│   │                               │                         │          │
│   └─ skills/ ◄───────────────────│  ┌───────────────────┐  │          │
│       (技能库)                    │  │ using-superpowers │  │          │
│                                   │  │   (入口技能)       │  │          │
│                                   │  └─────────┬─────────┘  │          │
│                                   │            │ 调用       │          │
│                                   │            ▼            │          │
│                                   │  ┌───────────────────┐  │          │
│                                   │  │  Superpowers 技能  │  │          │
│                                   │  │  (通用流程)        │  │          │
│                                   │  └───────────────────┘  │          │
│                                   │            │            │          │
│                                   │            ▼            │          │
│                                   │  ┌───────────────────┐  │          │
│                                   │  │   领域技能         │  │          │
│                                   │  │ (game-development) │  │          │
│                                   │  └───────────────────┘  │          │
│                                   └─────────────────────────┘          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 技能调用关系

```
                              用户请求
                                 │
                                 ▼
                    ┌───────────────────────┐
                    │   using-superpowers   │
                    │     (入口判断)         │
                    └───────────┬───────────┘
                                │
              ┌─────────────────┼─────────────────┐
              ▼                 ▼                 ▼
    ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
    │  brainstorming  │ │  systematic-    │ │ test-driven-    │
    │   (创建功能)    │ │   debugging     │ │ development     │
    └────────┬────────┘ │   (修复Bug)     │ │  (实现功能)     │
             │          └─────────────────┘ └─────────────────┘
             ▼
    ┌─────────────────────────────────────────────┐
    │              领域技能（提供专业知识）          │
    │  ┌───────────────┐  ┌───────────────────┐  │
    │  │ game-design   │  │ game-development  │  │
    │  │ (34个参考)    │  │   (编排器)         │  │
    │  └───────────────┘  └─────────┬─────────┘  │
    │                               │            │
    │              ┌────────────────┼────────┐   │
    │              ▼                ▼        ▼   │
    │         2d-games        3d-games   vr-ar   │
    └─────────────────────────────────────────────┘
             │
             ▼
    ┌─────────────────┐
    │  writing-plans  │
    │   (编写计划)     │
    └────────┬────────┘
             │
             ▼
    ┌─────────────────┐
    │ executing-plans │
    │   (执行计划)     │
    └────────┬────────┘
             │
             ▼
    ┌─────────────────────────────────────────────┐
    │              项目特定技能                    │
    │  ┌─────────────────┐ ┌─────────────────┐   │
    │  │ unity-mcp-      │ │ unity-test-     │   │
    │  │ orchestrator    │ │ framework       │   │
    │  └─────────────────┘ └─────────────────┘   │
    └─────────────────────────────────────────────┘
```

---

## 一、目录结构

```
.trae/
├── mcp.json                    # MCP 服务器配置
├── agents/                     # 自定义 Agent
│   └── code-reviewer.md
└── skills/                     # 技能库
    │
    │  # ===== Superpowers 技能（通用流程）=====
    ├── using-superpowers/      # 入口技能（必需）
    ├── brainstorming/          # 头脑风暴
    ├── writing-plans/          # 编写实施计划
    ├── executing-plans/        # 执行实施计划
    ├── test-driven-development/    # 测试驱动开发
    ├── systematic-debugging/   # 系统化调试
    ├── verification-before-completion/  # 完成前验证
    ├── dispatching-parallel-agents/   # 并行代理调度
    ├── subagent-driven-development/   # 子代理驱动开发
    ├── receiving-code-review/  # 接收代码审查
    ├── requesting-code-review/ # 请求代码审查
    ├── finishing-a-development-branch/ # 完成开发分支
    ├── using-git-worktrees/    # Git Worktree 使用
    │
    │  # ===== 项目特定技能 =====
    ├── unity-mcp-orchestrator/ # Unity MCP 操作指南
    ├── unity-test-framework/   # Unity 测试框架
    │
    │  # ===== 领域技能 =====
    ├── game-design/            # 游戏设计（独立，34个参考文件）
    └── game-development/       # 游戏开发编排器
        ├── 2d-games/
        ├── 3d-games/
        ├── game-design/        # 基础游戏设计原则（子技能）
        ├── game-art/
        ├── game-audio/
        ├── mobile-games/
        ├── pc-games/
        ├── web-games/
        ├── vr-ar/
        └── multiplayer/
```

---

## 二、核心配置文件

### AGENTS.md

放在项目根目录，和 `.trae/` 同级。

里面写的是项目级 AI 指令：工作流程、代码规范、偏好设置这些。

### mcp.json

放在 `.trae/mcp.json`，配置 MCP 服务器连接：

```json
{
  "mcpServers": {
    "unityMCP": { "url": "http://localhost:8080/mcp" }
  }
}
```

---

## 三、技能分类

### 3.1 Superpowers 技能（通用流程）

来自 superpowers 技能集，任何项目都能用。

| 技能 | 什么时候用 | 干什么 |
|------|-----------|--------|
| **using-superpowers** | 对话开始时 | 判断要不要调用其他技能 |
| **brainstorming** | 创建功能前 | 撸需求、出方案 |
| **writing-plans** | 需求明确了，写代码前 | 出实施计划 |
| **executing-plans** | 有计划后 | 一步步执行 |
| **test-driven-development** | 实现功能时 | 先写测试再写代码 |
| **systematic-debugging** | 遇到 bug 时 | 系统化找根因 |
| **verification-before-completion** | 说完成前 | 验证真完成了 |
| **dispatching-parallel-agents** | 有 2+ 独立任务时 | 并行调度代理 |
| **subagent-driven-development** | 执行计划时 | 子代理驱动开发 |
| **receiving-code-review** | 收到审查反馈时 | 处理意见 |
| **requesting-code-review** | 完成主要步骤后 | 请求代码审查 |
| **finishing-a-development-branch** | 实现完成后 | 决定怎么集成 |
| **using-git-worktrees** | 需要隔离工作时 | 创建隔离工作树 |

### 3.2 项目特定技能

| 技能 | 干什么 |
|------|--------|
| **unity-mcp-orchestrator** | Unity MCP 工具最佳实践 |
| **unity-test-framework** | Unity 测试框架 asmdef 配置 |

### 3.3 领域技能

| 技能 | 干什么 |
|------|--------|
| **game-design** | 游戏设计，独立技能，有 34 个参考文件 |
| **game-development** | 游戏开发编排器，路由到子技能 |
| **game-development/2d-games** | 2D 游戏开发模式 |
| **game-development/3d-games** | 3D 游戏开发模式 |
| **game-development/game-design** | 基础游戏设计原则：核心循环、GDD、玩家心理 |
| **game-development/mobile-games** | 移动端游戏 |
| **game-development/web-games** | 网页游戏 |
| **game-development/vr-ar** | VR/AR 开发 |
| **game-development/multiplayer** | 多人游戏网络 |

> 注意区分 `game-design`（顶层技能，34个参考文件）和 `game-development/game-design`（编排器子技能，基础原则）。

### 3.4 game-design 参考资料详情

| 主题 | 文件 |
|------|------|
| 角色优化设计 | `character-optimization-design.md` + 示例 |
| 动态难度调整 | `dynamic-difficulty-adjustment.md` + 示例 |
| 体验节奏结构 | `experience-pacing-structure.md` + 注意力管理 |
| 游戏能力与谜题 | `game-competency-puzzle-design.md` + 示例 |
| 游戏设计方法论 | `game-design-methodology.md` + 方法详情 |
| 设计原则参考 | `game-design-principles-reference.md` + 完整索引 |
| 开发规划 | `game-development-planning.md` + 规划示例 |
| 玩家心理决策 | `player-psychology-decisions.md` + 偏见示例 |
| 强化反馈系统 | `reinforcement-feedback-systems.md` + 奖励系统 |
| 协同与主题设计 | `synergy-thematic-design.md` + 主题示例 |
| 视觉玩家引导 | `visual-player-guidance.md` + 示例 |
| 倍增/减半平衡 | `doubling-halving-balance.md` |
| 环境叙事技巧 | `environmental-storytelling-technique.md` |
| 费茨定律（UI瞄准） | `fitts-law-ui-aiming.md` |
| 心流状态设计 | `flow-state-design-framework.md` |
| 基本归因错误测试 | `fundamental-attribution-error-testing.md` |
| 原型测试 | `game-prototyping-testing.md` |
| 团队管理 | `game-team-management.md` |
| 黄金比例设计 | `golden-ratio-design.md` |
| 希克定律（决策优化） | `hicks-law-decision-optimization.md` |
| 玩家错误处理 | `player-error-handling.md` |
| 以用户为中心设计 | `user-centered-design.md` |
| 索引文件 | `index.md`, `skill.md` |