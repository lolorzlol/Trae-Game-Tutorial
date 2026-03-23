# MCP 与 Skill 教程

本教程介绍 MCP（Model Context Protocol）和 Skill（技能）两个核心概念。

---

# 一、MCP（Model Context Protocol）

## 1. 什么是 MCP？

**MCP** 是 Anthropic 提出的开放协议，用于连接 AI 与外部数据源和工具。

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   AI Client     │ ←→  │   MCP Server    │ ←→  │  External Data  │
│  (Claude/Trae)  │     │  (中间层服务)    │     │   (数据源/工具)  │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

**核心组件：**
| 组件 | 说明 |
|------|------|
| **Tools** | 可执行的函数/操作 |
| **Resources** | 可读取的数据源 |
| **Prompts** | 预定义的提示模板 |

## 2. 配置 MCP

在 `settings.json` 中添加：

```json
{
  "mcpServers": {
    "server-name": {
      "command": "node",
      "args": ["path/to/server.js"]
    }
  }
}
```

## 3. MCP Server

| Server | 功能 |
|--------|------|
| **github** | GitHub API |
| **unity-mcp** | Unity 编辑器控制 |

---

# 二、Skill（技能）

## 1. 什么是 Skill？

**Skill** 是预定义的知识和工作流程，指导 AI 完成特定任务。

| 特性 | 普通提示词 | Skill |
|------|-----------|-------|
| 复用性 | 一次性 | 可跨项目复用 |
| 结构化 | 非结构化文本 | 有固定格式 |
| 可发现性 | 需手动输入 | 自动发现加载 |

## 2. Skill 类型

| 类型 | 说明 | 示例 |
|------|------|------|
| **严格型** | 必须严格遵循流程 | TDD, debugging |
| **灵活型** | 根据上下文调整 | patterns, design |

## 3. 使用 Skill

**显式调用：**
```
/brainstorming
/systematic-debugging
```

**自动触发：** AI 根据任务描述自动匹配。

## 4. 元技能

### find-skills
发现和安装新 Skill。

### skill-creator
创建、修改和优化 Skill。

**核心方法：TDD for Skills**
```
RED → 编写测试场景，观察失败行为
GREEN → 编写 Skill，使测试通过
REFACTOR → 关闭漏洞，优化内容
```

## 5. SKILL.md 结构

```markdown
---
name: skill-name
description: Use when [触发条件]
---

# Skill Name

## Overview
核心原则（1-2 句）

## When to Use
适用场景

## Core Pattern
具体方法和示例

## Common Mistakes
常见错误
```

**命名规范：**
- 只用字母、数字、连字符
- 动词开头：`creating-skills`
- description 只描述触发条件，不描述流程

## 6. pdf2skill

将 PDF 书籍转换为 Skill。

参考：https://mp.weixin.qq.com/s/ci7e-uukIjnlozofqQLjrQ

---

# 三、MCP 与 Skill 协同

| 特性 | MCP | Skill |
|------|-----|-------|
| **本质** | 工具和数据接口 | 知识和工作流程 |
| **作用** | 让 AI 能"做"事 | 让 AI 会"做"事 |

**示例：Unity 自动化测试**
```
MCP 提供能力：创建对象、运行测试、截图
Skill 提供流程：先写测试 → 再实现 → 验证
```

---

# 四、参考资源

- MCP 官方：https://modelcontextprotocol.io/
- MCP Servers：https://github.com/modelcontextprotocol/servers
- 本项目 Skills：`Tutorial-1/Test/.trae/skills/`