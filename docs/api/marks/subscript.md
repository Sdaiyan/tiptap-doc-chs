# 下标

使用此扩展可以将文本呈现为下标。 如果在编辑器的初始内容中传递了`<sub>`或具有`vertical-align：sub`的文本作为内联样式，两者都会相应地呈现。

::: 警告
阅读`Editor`实例内容时，此扩展将生成相应的“<sub> ”HTML标签。无论采用何种方法，所有下标文字都将标准化为“<sub>”HTML标签。
:::

## 安装

```bash
npm install @tiptap/extension-subscript
```

## 设置
### HTMLAttributes

应将其添加到呈现的HTML标记中的自定义HTML属性。

```js
Subscript.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setSubscript()
将文字标记为下标。

```js
editor.commands.setSubscript()
```

### toggleSubscript()
切换下标标记。

```js
editor.commands.toggleSubscript()
```

### unsetSubscript()
删除下标标记。

```js
editor.commands.unsetSubscript()
```

## 快捷键
| Command           | Windows/Linux      | macOS          |
| ----------------- | ------------------ | -------------- |
| toggleSubscript() | `Control`&nbsp;`,` | `Cmd`&nbsp;`,` |

## 源代码
[packages/extension-subscript/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-subscript/)

## 用法
https://embed.tiptap.dev/preview/Marks/Subscript