# 历史记录

[![Version](https://img.shields.io/npm/v/@tiptap/extension-history.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-history)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-history.svg)](https://npmcharts.com/compare/@tiptap/extension-history?minimal=true)

这个扩展功能提供了历史记录支持。所有文档的更改都会被跟踪，并可以通过“撤销”进行删除。撤销的更改可以通过“重做”再次应用。

## 安装

```bash
npm install @tiptap/extension-history
```

## 设置

### depth

在废弃最早的事件之前记录的历史事件数量。默认为 100。

默认值：`100`

```js
History.configure({
  depth: 10,
})
```

### newGroupDelay

更改之间的延迟时间（毫秒），之后会启动新的组。当更改不相邻时，始终会启动新组。

默认值：`500`

```js
History.configure({
  newGroupDelay: 1000,
})
```

## 命令

### undo()

撤销上一次更改。

```js
editor.commands.undo()
```

### redo()

重做上一次更改。

```js
editor.commands.redo()
```

## 快捷键

| 命令    | Windows/Linux                                                                            | macOS                                                                        |
| ------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| undo()  | `Control`&nbsp;`Z`<br>`Control`&nbsp;`я`                                                 | `Cmd`&nbsp;`Z`<br>`Cmd`&nbsp;`я`                                             |
| redo()  | `Shift`&nbsp;`Control`&nbsp;`Z`<br>`Control`&nbsp;`Y`<br>`Shift`&nbsp;`Control`&nbsp;`я` | `Shift`&nbsp;`Cmd`&nbsp;`Z`<br>`Cmd`&nbsp;`Y`<br>`Shift`&nbsp;`Cmd`&nbsp;`я` |

## 源代码

[packages/extension-history/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-history/)

## 用法

https://embed.tiptap.dev/preview/Extensions/History