# Obsidian Fragment Diary Workflow

一套把“随手碎念 → 每日日记 → GPT 批注与整体回应”串起来的 Obsidian / iPhone / Codex 工作流。

它解决的问题很简单：

> 白天不用憋成完整文章，只要把脑子里的碎片扔进 `## 碎念流`；晚上或每天 00:00，让 GPT 读完整天的碎念，在原文上少量批注，并在 `## 长文` 写一篇整体回应。

## 核心效果

每天一个 Obsidian 日记文件：

```md
# 2026-06-05

## 碎念流

- 15:03
  今天突然想到一句话。

## 长文
```

- `## 碎念流`：收集零散想法、吐槽、灵感、图片、截图。
- `## 长文`：由 GPT 写入整体回应。
- Hover Reveal 批注：GPT 可以直接挂在碎念原文旁边轻轻插嘴。

## 工作流总览

```text
电脑 / 手机 / 快捷指令记录碎念
        ↓
写入 Obsidian 每日笔记的 ## 碎念流
        ↓
Codex Automation 每天 00:00 调用 $diary-response
        ↓
GPT 读取昨天的碎念与可读图片
        ↓
少量添加 Hover Reveal 批注
        ↓
在 ## 长文 写整体回应并保存
```

## 仓库内容

```text
docs/
├── private-fragment-flow-guide.md   # Obsidian + iPhone 快捷指令搭建教程
├── codex-automation.md              # 每天 00:00 自动运行的 prompt
├── hover-reveal-annotations.md      # GPT 悬浮批注语法与风格规则
└── design-notes.md                  # 需求迭代与设计取舍

templates/
├── daily-note-template.md           # 每日笔记模板
└── insert-fragment-templater.md      # Templater 插入碎念模板

skills/
└── diary-response/SKILL.md          # Codex Skill：读取碎念并写 GPT 回应

snippets/
└── hover-reveal-mobile-clean.css    # 手机端 Hover Reveal 样式优化

examples/
└── example-daily-note.md            # 示例日记结构
```

## 快速开始

### 1. 建立每日笔记模板

把 `templates/daily-note-template.md` 放到 Obsidian 模板文件夹中。

模板内容：

```md
# {{date:YYYY-MM-DD}}

## 碎念流

## 长文
```

### 2. 建立插入碎念模板

把 `templates/insert-fragment-templater.md` 放到 Templater 模板文件夹中。

模板内容：

```md
- <% tp.date.now("HH:mm") %>  
  
```

### 3. 配置 iPhone 快捷指令

按 `docs/private-fragment-flow-guide.md` 配置：

- 输入文字；
- 可选加图片；
- 可选打开 Obsidian；
- 不打开时静默写入文件；
- 打开时通过 Advanced URI 写入 `## 碎念流`。

### 4. 安装 / 同步 Codex Skill

把 `skills/diary-response/SKILL.md` 放到项目级 skill 目录，例如：

```text
.agents/skills/diary-response/SKILL.md
```

之后就可以在 Codex 里调用：

```text
使用 $diary-response 处理昨天的 Obsidian 日记。
```

### 5. 设置 Codex Automation

见 `docs/codex-automation.md`。

推荐 prompt：

```text
每天 00:00 运行。

使用 $diary-response 处理昨天的 Obsidian 日记。
如果没有明确指定路径，请根据当前日期计算昨天，目标路径格式为：
01日记/YYYY-MM-DD.md

完成后直接写回文件。
```

## GPT 回应的写作原则

`## 长文` 不是把碎念改写成用户日记，而是 GPT 的整体回应。

它不应该是：

- 逐条总结；
- “关于 A / 关于 B / 关于 C”；
- 阅读理解；
- 心理咨询；
- 正式书信；
- 把一天包装成一个漂亮主题。

它应该更像：

- GPT 完整读过这一天之后写下来的回应；
- 能看见文本下面的情绪、欲望、矛盾和问题；
- 有一点联想，有一点判断，有一点温度；
- 能提出明天或下周可以考虑、尝试、创造、暂时放过的东西；
- 如果写不出灵气，宁可朴素，不要用力证明自己聪明。

## Hover Reveal 批注语法

```md
[原文中可见的句子或短语]{gpt：批注内容}
```

例子：

```md
[今天的风有点冷，但我居然很想把它记下来。]{gpt：这个句子很轻，但它留下的是那一秒真的存在过。}
```

## 隐私说明

这个仓库只保存可复用的教程、模板、prompt、skill 和样式片段。

不要上传：

- 真实日记；
- 真实碎念；
- 真实照片或截图；
- 私人 Obsidian vault 内容；
- 含有个人隐私的自动化运行结果。
