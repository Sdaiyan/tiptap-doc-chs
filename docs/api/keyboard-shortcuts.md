---
tableOfContents: true
---

# 键盘快捷键

## 简介

Tiptap 默认提供了一些合理的键盘快捷键。根据您使用的场景，您可能需要更改这些键盘快捷键以符合您的喜好。让我们来看一下我们为您定义的快捷键，并向您展示如何更改它们！

## 预定义的键盘快捷键

大多数核心扩展都注册了自己的键盘快捷键。根据您使用的扩展集合，下面列出的键盘快捷键可能并不适用于您的编辑器。

### 基本操作

| 命令       | Windows/Linux         | macOS             |
| ---------- | --------------------- | ----------------- |
| 复制       | `Control` `C`         | `Cmd` `C`         |
| 剪切       | `Control` `X`         | `Cmd` `X`         |
| 粘贴       | `Control` `V`         | `Cmd` `V`         |
| 无格式粘贴 | `Control` `Shift` `V` | `Cmd` `Shift` `V` |
| 撤销       | `Control` `Z`         | `Cmd` `Z`         |
| 重做       | `Control` `Shift` `Z` | `Cmd` `Shift` `Z` |
| 插入换行   | `Shift` `Enter`       | `Shift` `Enter`   |

### 文本格式

| 命令   | Windows/Linux         | macOS             |
| ------ | --------------------- | ----------------- |
| 粗体   | `Control` `B`         | `Cmd` `B`         |
| 斜体   | `Control` `I`         | `Cmd` `I`         |
| 下划线 | `Control` `U`         | `Cmd` `U`         |
| 删除线 | `Control` `Shift` `X` | `Cmd` `Shift` `X` |
| 高亮   | `Control` `Shift` `H` | `Cmd` `Shift` `H` |
| 代码块 | `Control` `E`         | `Cmd` `E`         |

### 段落格式

| 命令             | Windows/Linux         | macOS             |
| ---------------- | --------------------- | ----------------- |
| 应用普通文本样式 | `Control` `Alt` `0`   | `Cmd` `Alt` `0`   |
| 应用一级标题样式 | `Control` `Alt` `1`   | `Cmd` `Alt` `1`   |
| 应用二级标题样式 | `Control` `Alt` `2`   | `Cmd` `Alt` `2`   |
| 应用三级标题样式 | `Control` `Alt` `3`   | `Cmd` `Alt` `3`   |
| 应用四级标题样式 | `Control` `Alt` `4`   | `Cmd` `Alt` `4`   |
| 应用五级标题样式 | `Control` `Alt` `5`   | `Cmd` `Alt` `5`   |
| 应用六级标题样式 | `Control` `Alt` `6`   | `Cmd` `Alt` `6`   |
| 有序列表         | `Control` `Shift` `7` | `Cmd` `Shift` `7` |
| 无序列表         | `Control` `Shift` `8` | `Cmd` `Shift` `8` |
| 任务列表         | `Control` `Shift` `9` | `Cmd` `Shift` `9` |
| 引用块           | `Control` `Shift` `B` | `Cmd` `Shift` `B` |
| 左对齐           | `Control` `Shift` `L` | `Cmd` `Shift` `L` |
| 居中对齐         | `Control` `Shift` `E` | `Cmd` `Shift` `E` |
| 右对齐           | `Control` `Shift` `R` | `Cmd` `Shift` `R` |
| 两端对齐         | `Control` `Shift` `J` | `Cmd` `Shift` `J` |
| 代码块           | `Control` `Alt` `C`   | `Cmd` `Alt` `C`   |
| 下标             | `Control` `,`         | `Cmd` `,`         |
| 上标             | `Control` `.`         | `Cmd` `.`         |

### 文本选择

| 命令                 | Windows/Linux         | macOS             |
| -------------------- | --------------------- | ----------------- |
| 全选                 | `Control` `A`         | `Cmd` `A`         |
| 向左扩展选择一个字符 | `Shift` `←`           | `Shift` `←`       |
| 向右扩展选择一个字符 | `Shift` `→`           | `Shift` `→`       |
| 向上扩展选择一行     | `Shift` `↑`           | `Shift` `↑`       |
| 向下扩展选择一行     | `Shift` `↓`           | `Shift` `↓`       |
| 扩展选择到文档开头   | `Control` `Shift` `↑` | `Cmd` `Shift` `↑` |
| 扩展选择到文档结尾   | `Control` `Shift` `↓` | `Cmd` `Shift` `↓` |

## 覆盖键盘快捷键

键盘快捷键可以是字符串，比如 `'Shift-Control-Enter'`。按键基于可以出现在 `event.key` 中的字符串，并用 `-` 连接起来。有一个小工具叫做 [keycode.info](https://keycode.info/)，可以交互地展示 `event.key`。

使用小写字母来表示字母键（或者大写字母，如果需要按下 Shift 键）。您可以使用 `Space` 作为 ` ` 的别名。

修改键可以以任何顺序给出。`Shift`、`Alt`、`Control` 和 `Cmd` 都是被识别的。对于通过按住 Shift 创建的字符，`Shift` 前缀是隐含的，不应该显式添加。

您可以在 Mac 上使用 `Mod` 作为 `Cmd` 的缩写，在其他平台上使用 `Control`。

以下是一个示例，说明如何覆盖现有扩展的键盘快捷键：

```js
// 1. 导入扩展
import BulletList from '@tiptap/extension-bullet-list'

// 2. 覆盖键盘快捷键
const CustomBulletList = BulletList.extend({
  addKeyboardShortcuts() {
    return {
      // ↓ 您的新键盘快捷键
      'Mod-l': () => this.editor.commands.toggleBulletList(),
    }
  },
})

// 3. 将自定义扩展添加到您的编辑器
new Editor({
  extensions: [
    CustomBulletList(),
    // …
  ],
})
```
