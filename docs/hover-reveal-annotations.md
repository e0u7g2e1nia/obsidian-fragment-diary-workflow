# Hover Reveal 批注规则

这个工作流使用 Obsidian Hover Reveal 插件，把 GPT 的轻量回应挂在 `## 碎念流` 原文上。

## 语法

```md
[原文中可见的句子或短语]{gpt：批注内容}
```

中括号里的内容本身就是正文，不要再复制一遍。

## 好的例子

```md
[今天的风有点冷，但我居然很想把它记下来。]{gpt：这个句子很轻，但它留下的是那一秒真的存在过。}
```

## 批注应该像什么

像在旁边轻轻插嘴：

- 喜欢一句话，就简单说喜欢；
- 不太同意，就轻轻杠一下；
- 有联想，就说一句联想到什么；
- 有提醒，就短短补一下；
- 没话说，就不要硬批。

## 不应该像什么

不要：

- 每条都批；
- 重复原文；
- 把批注写成阅读理解；
- 用力过猛地假装同频；
- 生硬标注“这是共情/这是反驳/这是联想”；
- 为了证明自己懂而装聪明。

## 手机显示优化

如果手机上 Hover Reveal 批注太丑，可以启用本仓库里的 CSS snippet：

```text
snippets/hover-reveal-mobile-clean.css
```

放到 Obsidian vault 的：

```text
.obsidian/snippets/hover-reveal-mobile-clean.css
```

然后在 Obsidian 设置里启用该 CSS snippet。
