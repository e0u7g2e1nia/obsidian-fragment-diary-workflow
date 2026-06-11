# Obsidian 私密碎念流搭建教程

这是一套适合新手的 Obsidian 私密碎念流搭建方法：电脑端可以快速记录，手机 Obsidian 内可以快速编辑，iPhone 快捷指令可以一键写入，还能选择是否加图片、是否打开 Obsidian。

## 最终效果

每天一个日记文件，例如：

```text
2026-06-05.md
```

文件里有两个固定区域：

```md
## 碎念流

## 长文
```

- `## 碎念流`：放随手想到的短句、吐槽、灵感、碎片化想法、图片。
- `## 长文`：由 Codex / GPT 自动写入整体回应。

> 注意：`碎念流` 和 `长文` 这两个标题要保持一致。快捷指令和 skill 都靠它们定位。

## 一、刚下载 Obsidian：先搭笔记库

### 1. 新建 Vault

打开 Obsidian，新建一个 Vault / 笔记库。

如果要用 iPhone 快捷指令直接写文件，建议把 Vault 放在 iCloud Drive 里。这样 iPhone 的“文件”App 和快捷指令才能找到它。

### 2. 新建三个文件夹

```text
日记
模板
附件
```

最终结构：

```text
我的笔记库/
├── 日记/
├── 模板/
└── 附件/
```

### 3. 设置附件默认位置

Obsidian → Settings → Files and links → Default location for new attachments → 选择指定文件夹 → 填：

```text
附件
```

## 二、电脑端：Daily Notes + Templater

### 1. 开启 Daily Notes

Settings → Core plugins → 打开 Daily notes。

### 2. 设置 Daily Notes

Settings → Daily notes：

```text
Date format: YYYY-MM-DD
New file location: 日记
Template file location: 模板/日记模板
```

### 3. 新建日记模板

在 `模板` 文件夹里新建：

```text
日记模板.md
```

内容：

```md
# {{date:YYYY-MM-DD}}

## 碎念流

## 长文
```

### 4. 安装 Templater

Settings → Community plugins → Browse → 搜索 Templater → Install → Enable。

### 5. 设置 Templater 模板文件夹

Settings → Templater → Template folder location → 选择：

```text
模板
```

### 6. 新建“插入碎念”模板

在 `模板` 文件夹里新建：

```text
插入碎念.md
```

内容：

```md
- <% tp.date.now("HH:mm") %>  
  
```

不要加 `tp.file.cursor()`，有些环境里会原样显示，容易把笔记搞乱。

### 7. 设置快捷命令

Settings → Templater → Template hotkeys → Add new hotkey for template → 选择 `模板/插入碎念.md`。

然后到 Settings → Hotkeys 里绑定快捷键。

推荐：

- `⌘ + J`：打开今天日记；
- `⌘ + Enter`：插入一条带时间的碎念。

## 三、手机 Obsidian 内部快速记录

### 1. 开启 Command palette

手机 Obsidian → Settings → Core plugins → 打开 Command palette。

### 2. 置顶常用命令

Settings → Command palette → New pinned command。

建议置顶：

```text
Open today's daily note
Templater: Insert 插入碎念
```

### 3. 设置下滑 Quick Action

Settings → Toolbar → Configure mobile Quick Action。

推荐设为：

```text
Open today's daily note
```

### 4. 把“插入碎念”加入编辑工具栏

Settings → Toolbar → Manage toolbar options → Add global command → 搜索 Templater 的“插入碎念”命令 → 添加到工具栏。

## 四、iPhone 快捷指令：一键写入碎念

最终逻辑：

```text
输入文字 → 可选加图片 → 问要不要打开 Obsidian → 不打开就静默写入文件 → 要打开就用 Advanced URI 写入并打开
```

### 0. 安装 Advanced URI

Obsidian → Settings → Community plugins → 搜索 Advanced URI → 安装并启用。

“要打开 Obsidian”分支会用到 Advanced URI；“不要打开”分支不会用它。

### 1. 新建快捷指令

打开 iPhone 自带“快捷指令”App → 新建快捷指令 → 命名为：

```text
记一条碎念
```

### 2. 输入文字

动作：请求输入。

示例：

```text
通过“写吧！”请求 文本
```

### 3. 获取并格式化当前时间

添加：当前日期。

然后添加三个“格式化日期”：

```text
HH:mm
```

用于每条碎念前面的时间。

```text
yyyy-MM-dd
```

用于今天的日记文件名。

```text
yyyy-MM-dd-HHmmss
```

用于图片文件名。

三个“格式化日期”的输入都必须是“当前日期”。如果它们吃到文本，就会报错：无法将文本转换为日期。

### 4. 生成纯文字条目

文本动作：

```text
- [记录时间]
  [请求输入]
```

然后：

```text
将变量 最终条目 设为 文本
```

### 5. 菜单：有没有照片？

添加“从菜单中选取”：

```text
有照片吗？
- 没有
- 有
```

“没有”分支保持空着。

“有”分支：

```text
选择照片
将照片转换为 JPEG
将转换后的图像名称设为 [图片时间戳].jpg
将重新命名的项目保存到 附件
```

然后重新生成带图条目：

```md
- [记录时间]
  [请求输入]

![[重新命名的项目.jpg]]
```

如果图片不显示，可以改成：

```md
![[附件/重新命名的项目.jpg]]
```

### 6. 为 Advanced URI 准备编码变量

菜单结束后：

```text
URL 编码 最终条目
文本：我的笔记库
URL 编码 Vault 名
文本：碎念流
URL 编码标题名
```

`我的笔记库` 要换成自己的 Vault 名。`碎念流` 不要带 `##`。

### 7. 菜单：要打开 Obsidian 吗？

添加第二个菜单：

```text
要打开 Obsidian 吗？
- 不要
- 要
```

### 8. 不打开 Obsidian：静默写入

这一支不能有 `打开 URL`，也不能有 `obsidian://...`。

逻辑：

1. 文本：`[今天日期].md`。
2. 从路径 `[今天文件名]` 获取 `日记` 中的文件。
3. 计算文件中项目数量。
4. 如果计数是 0，说明今天日记还不存在，新建：

```md
## 碎念流

[最终条目]

## 长文
```

5. 否则，说明今天日记已经存在，把文件中的 `## 长文` 替换为：

```md
[最终条目]

## 长文
```

6. 保存更新后的文本到 `日记/[今天日期].md`，并开启覆盖。

### 9. 要打开 Obsidian：Advanced URI

拼接：

```text
obsidian://adv-uri?vault=[编码后的Vault名]&daily=true&heading=[编码后的标题名]&data=[编码后的最终条目]&mode=append
```

然后“打开文本”。

## 五、测试顺序

1. 测试电脑端：打开今天日记，Templater 是否能插入当前时间。
2. 测试手机 Obsidian 内部：下滑打开今天日记，点工具栏里的插入碎念命令。
3. 测试快捷指令：无图 + 不打开。
4. 测试快捷指令：有图 + 不打开。
5. 测试快捷指令：无图 / 有图 + 要打开。

测试时一次只改一个地方。不要同时改日期、图片、打开方式、文件路径。

## 六、常见问题

### 无法将文本转换为日期

检查三个“格式化日期”动作，输入都必须是“当前日期”。

### 选“不打开”还是跳到 Obsidian

说明 `打开 URL` 或 `obsidian://adv-uri...` 放错位置了。“不要”分支里只能有文件写入动作。

### 第一次写入当天日记失败

当天日记还不存在。要在“不要”分支里加“如果计数是 0”的新建文件逻辑。

### 已有日记时写入失败

替换 `## 长文` 后，一定要加“保存到文件”。

### 图片不显示

检查：

- 图片是否保存进 `附件` 文件夹；
- 图片名是否有 `.jpg` 后缀；
- 是否需要写成 `![[附件/xxx.jpg]]`。

### Advanced URI 写入失败

检查：

- Advanced URI 是否安装并启用；
- Vault 名是否正确；
- `heading=碎念流` 是否和日记标题完全一致；
- 最终条目是否 URL 编码。
