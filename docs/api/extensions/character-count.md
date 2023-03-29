# CharacterCount
[![Version](https://img.shields.io/npm/v/@tiptap/extension-character-count.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-character-count)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-character-count.svg)](https://npmcharts.com/compare/@tiptap/extension-character-count?minimal=true)

`CharacterCount` 扩展限制允许的字符数量，还能返回字符数和单词数。就是这样，没有更多的东西了。

## 安装
```bash
npm install @tiptap/extension-character-count
```

## 设置

### limit

允许的最大字符数。

默认值：`null`

```js
CharacterCount.configure({
  limit: 240,
})
```

### mode

计算字数的模式。

默认值：`'textSize'`

```js
CharacterCount.configure({
  mode: 'nodeSize',
})
```

## 存储

### characters()
获取当前文档中字符数。

```js
editor.storage.characterCount.characters()

// 获取特定节点的大小。
editor.storage.characterCount.characters({ node: someCustomNode })

// 覆盖默认的 `mode`。
editor.storage.characterCount.characters({ mode: 'nodeSize' })
```

### words()
获取当前文档中单词数。

```js
editor.storage.characterCount.words()

// 获取特定节点的单词数。
editor.storage.characterCount.words({ node: someCustomNode })
```

## 源码
[packages/extension-character-count/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-character-count/)

## 用法
https://embed.tiptap.dev/preview/Extensions/CharacterCount