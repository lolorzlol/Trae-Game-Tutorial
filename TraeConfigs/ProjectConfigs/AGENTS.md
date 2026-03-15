
 # Workflow Orchestration

  ## 操作要求
  - 调用mcp失败时，优先根据调用返回的*信息(message)*, 调整调用参数重新执行mcp调用。
  - 开发过程按照*测试驱动开发（TDD）*进行。
  - 开发过程中及时读取unity编辑器的*Console*窗口内容，检查是否有报错
  - 任何对场景的编辑（如搭建场景），直接通过*unityMCP*来做，尽量避免用脚本配置
  - 使用unityMCP时，先载入*unity-mcp-helper*技能，了解*unityMCP*具有的编辑器操作功能。
  - 使用git做版本管理

  ## Plan Mode Orchestration
  - Non-trivial tasks (3+ steps or architecture decisions) must enter plan mode
  - If things go off track, stop and replan—don't push through
  - If bugs or frustration accumulate, stop and replan
  - Write detailed specs as input to reduce ambiguity
  - Use numbered steps

  ## Convert List to Subagents
  - Use subagents heavily to keep the main context window clean
  - Outsource research, exploration, and parallel analysis to subagents
  - Reduce cognitive load and separate concerns via subagents
  - One task per subagent, focused execution

  ## Self-Improvement Loop
  - After user correction: update `tasks/lessons.md` to record patterns
  - Write rules for yourself to prevent the same mistakes
  - Iterate improvements until error rate drops
  - Verify improvements each session, apply to relevant projects

  ## Verification Defaults On
  - Never mark a task complete until you've proven it works
  - Compare main branch to your changes when relevant
  - Always be ready to push to production, verify
  - Ask yourself "Would a senior engineer approve this?"
  - Do assertions, logs, test suite corrections

  ## Elegant Elegance - Balanced
  - For non-trivial changes: pause and ask "Is there a more elegant way?"
  - If a fix feels like a patch: "Now that I know everything, implement an elegant solution"
  - Skip this step for simple obvious fixes, don't over-engineer
  - Challenge your own work before committing

  ## Autonomous Bug Fixing
  - When you find a bug: fix it directly, don't ask for help
  - Point out logs, errors, failing tests, then resolve
  - User doesn't need to switch context
  - Proactively fix failing CI tests, no need to tell how

  ## Task Management
  1. Plan first: write plan to `tasks/todo.md` with checkboxes
  2. Validate plan: check before starting implementation
  3. Implement incrementally: check off each step as completed
  4. Explain changes: provide high-level summary for each step
  5. Document results: add review section in `tasks/todo.md`
  6. Record lessons: update `tasks/lessons.md` after corrections

  ## Core Principles
  - Simplicity first: each change should be as simple as possible, affecting minimal code
  - Don't be lazy: find root causes, no band-aid fixes, senior engineer standards
  - Minimal impact: changes should only involve what's necessary


## 技能依赖

| 时机 | 技能 |
|------|------|
| 使用unityMCP时| `unity-mcp-helper` |
| 使用unity-test-framework时| `unity-test-framework` |
| 进行测试驱动开发时| `test-driven-development` |

# 偏好
## 输入系统
- 使用旧的输入系统
## git
- 不使用*git worktree*。
- 及时更新git commit。

# 测试驱动开发（TDD）
- 按照*Red-Green-Refactor*方式，先写失败测试，代码开发完成后再通过编辑器TestRunner执行测试。通过测试后，通过code-review重构代码。
- 使用*unityMCP*在编辑器内通过TestRunner启动测试

# 游戏编辑器内测试
### 基本流程
- 通过play模式进入游戏
- 模拟输入
- 截图game窗口
- 对截图内容进行图像理解，并修复存在的问题

# 场景搭建
- 需要充分设计不同物体的大小和材质

# 常见问题
- 使用unit-test-framework时，没调用unity-test-framework技能导致编译错误

# 错误排查
- 首先查看Console窗口是否有编译错误

