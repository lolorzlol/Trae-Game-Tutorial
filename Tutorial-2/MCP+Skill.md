# 什么是 Skill，什么是 MCP

视频链接：https://www.bilibili.com/video/BV1ojfDBSEPv/

> 官方课程：https://anthropic.skilljar.com/introduction-to-agent-skills

---

## 元技能

管理 Skill 本身用的技能。

| 元技能 | 功能 |
|--------|------|
| **find-skills** | 发现和安装新 Skill |
| **skill-creator** | 创建、修改和优化 Skill |

### find-skills

想要某个功能，不确定有没有现成的 Skill？用这个。

```
/find-skills
```

然后描述你想要什么，AI 会帮你搜。

官网也可以手动搜：https://skills.sh/

### skill-creator

想自己写个 Skill，或者改现有的？用这个。

```
/skill-creator
```

---

## pdf2skill

> 官网：https://pdf2skills.memect.cn/quick-start

把 PDF 书籍、手册、行业报告转成 Skill 技能包的工具。

### 用法

**官网直接上传**

1. 打开 https://pdf2skills.memect.cn/quick-start
2. 上传 PDF 文件
3. 等编译完成（10-30 分钟，看文件大小）
4. 下载 `skills.zip`

### 它是怎么工作的

1. 文档解析 —— PDF 转成结构化文本
2. 语义拆解 —— 按语义密度和逻辑边界拆分，不按章节硬切
3. 逻辑建模 —— 搭建知识点之间的依赖关系
4. 技能封装 —— 输出标准 Skill 文件

### 适合什么场景

- 技术文档、专业书籍转 Skill
- 教程、规范文档转成可复用技能
- 让 AI 能参考专业知识

类似功能的开源替代：https://github.com/yusufkaraaslan/Skill_Seekers

---

## 参考资源

本项目 game-design 技能来自：https://mp.weixin.qq.com/s/ci7e-uukIjnlozofqQLjrQ?scene=1&click_id=46