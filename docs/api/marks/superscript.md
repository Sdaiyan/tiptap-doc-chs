# 上标
[![版本](https://img.shields.io/npm/v/@tiptap/extension-superscript.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-superscript)
[![下载量](https://img.shields.io/npm/dm/@tiptap/extension-superscript.svg)](https://npmcharts.com/compare/@tiptap/extension-superscript?minimal=true)

使用此扩展可将文本呈现为上标。如果你在编辑器的初始内容中传递 `<sup>` 或带有 `vertical-align: super` 的文本作为内联样式，这两个都会被相对应地呈现。

::: warning 限制
读取 `Editor` 实例的内容时，该扩展将生成相应的 `<sup>` HTML 标签。无论使用何种方法将文本设为上标，所有上标文本都将被标准化为 `<sup>` HTML 标签。
:::

## 安装
```bash
npm install @tiptap/extension-superscript
```

## 配置项

### HTMLAttributes
应添加到呈现的 HTML 标签中的自定义 HTML 属性。

```js
Superscript.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setSuperscript()
将文本设为上标。

```js
editor.commands.setSuperscript()
```

### toggleSuperscript()
切换上标标记。

```js
editor.commands.toggleSuperscript()
```

### unsetSuperscript()
取消上标标记。

```js
editor.commands.unsetSuperscript()
```

## 键盘快捷键
| 命令                | Windows/Linux      | macOS          |
| ------------------- | ------------------ | -------------- |
| toggleSuperscript() | `Control`&nbsp;`.` | `Cmd`&nbsp;`.` |

## 源代码
[packages/extension-superscript/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-superscript/)

## 用法
https://embed.tiptap.dev/preview/Marks/Superscript