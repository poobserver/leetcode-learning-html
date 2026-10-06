# LeetCode Cognitive Learning Skill

> 把一道 LeetCode 题变成可交互的认知训练，而不是再生成一份题解。

大多数 AI 刷题助手回答的是：**“这道题怎么做？”**

这个 Skill 进一步追问：**“怎样让我形成解题模型，并在没有答案的情况下重新写出来？”**

它把“看懂”设计成一段练习过程：

**题目 → 心智模型 → 反例 → 真实执行轨迹 → 手填关键逻辑 → 独立重写 → 迁移训练**

目标不是“我理解了这段代码”，而是“没有这段代码，我还能不能重新推出来”。学习页以可离线打开的 HTML 交付；HTML 是载体，认知训练闭环才是重点。

![认知训练组件图：心智模型、状态轨迹、手填代码、独立重写与迁移](assets/component-atlas.svg)

## 为什么不是普通 AI 题解？

普通刷题常常是：

```text
题目 → 看解释 → 看代码 → 感觉看懂了 → 下一题
```

这个 Skill 生成一套主动练习流程：

```text
题目
  → 建立心智模型
  → 用反例检验错误理解
  → 跟踪真实程序状态
  → 亲手补全关键逻辑
  → 收起参考，独立重写
  → 用变体题验证迁移
```

## 认知训练闭环

- **心智模型**：说明本题改变了哪种决策，以及它在更大的解题框架中处于什么位置。
- **反例**：用能击穿常见错误想法的输入检验理解。
- **真实轨迹**：运行参考算法，逐步展示状态、决策和不变量。
- **主动编码**：代码槽位初始为空；练习区与参考代码分开。
- **独立重写**：从公开函数签名和空白起点重新组织解法。
- **迁移训练**：在相近变体中辨认哪些思想保留、哪些规则改变。

错误答案可以重试，模块可以自由进入；页面不预填代码，也不保存跨次学习记录。

## 页面示例

以下是本 Skill 生成的 [LeetCode 704 二分查找训练页](examples/leetcode_704_learning.html)。完整页面还包含真实运行轨迹、手填槽位、参考复习、独立重写和迁移训练。

![桌面端示例：题目框架、认知梯度、状态视图与交互判断](assets/example-704.png)

## 30 秒开始

克隆仓库后，把整个目录提供给你的 Coding Agent，并要求它先阅读 `SKILL.md`：

```text
请先阅读 SKILL.md，然后把 LeetCode 226 翻转二叉树设计成一套认知训练。
使用中文和 Python，包含能暴露错误模型的反例、真实状态轨迹、空白代码槽位、
独立重写，以及迁移到一个结构相近但规则不同的问题。输出可离线打开的 HTML。
```

支持 Codex、Claude Code、Trae、Cursor、Cline、Aider 等工具。支持技能目录的工具可将本仓库作为技能安装；其他工具可以把目录加入项目规则，并要求 Agent 读取 `SKILL.md`。Claude Code 可复制到 `.claude/skills/leetcode-learning-html/`；Trae 等工具可在项目规则中引用该文件。

只有题号或链接时，Agent 应先核实题意、约束、函数签名和返回语义。遇到无法确认的题面，不编造题目细节。

## 命令行生成

也可以直接准备符合 [`references/content-schema.md`](references/content-schema.md) 的 `lesson.json`，不依赖任何 AI 编辑器：

```powershell
python scripts/build_lesson.py lesson.json --output output/lesson.html
node scripts/verify_lesson.cjs output/lesson.html
```

仓库中的完整示例可重新生成：

```powershell
python scripts/demo_binary_search.py --output-dir output
node scripts/verify_lesson.cjs output/leetcode_704_learning.html
```

## 设计原则

- 轨迹由运行的算法生成，不靠模型凭空编写每一步状态。
- 手填槽位与独立编辑器不自动填入答案；参考视图与练习区分开。
- 选项、导航、检查和参考入口绑定到明确动作，不从按钮文字猜行为。
- 学习模块可自由进入；查看参考或进入模块不算作掌握。
- 刷新页面或重新打开时重新开始；同一次访问中切换模块可保留草稿。
- 检查结果只陈述实际验证过的内容；没有真实运行器时，不把关键词匹配说成算法通过。

教学方法详见 [`references/teaching-design.md`](references/teaching-design.md)，页面字段见 [`references/content-schema.md`](references/content-schema.md)，交付前核对见 [`references/verification.md`](references/verification.md)。

## 仓库内容

```text
SKILL.md                 Agent 技能说明与生成规则
agents/openai.yaml       可选的 Codex 展示配置；Claude Code、Trae 等工具可忽略
assets/                  页面模板、样例截图与组件图
examples/                可打开的示例 HTML 和 lesson JSON
references/              教学设计、内容结构与验证要求
scripts/                 构建、示例生成和验证脚本
```

本 Skill 提炼了数组、链表、树、二分、图和动态规划训练页中的可迁移教学机制。每道新题都需要自己的模型、反例和证明，不会把示例题的算法模板直接套用过去。
