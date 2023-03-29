# 删除线

使用该扩展可以呈现 ~~删除线文本~~。如果你在编辑器的初始内容中传递了 `<s>`、`<del>`、`<strike>` 标签或具有内联 `style` 属性且设置为 `text-decoration: line-through` 的文本，则它们都将呈现相应的删除线文本。

在两个波浪线之间输入 <code>&Tilde;&Tilde;文本&Tilde;&Tilde;</code>，你打的文字将被奇妙的 ~~划掉~~。

::: warning 限制
当阅读`Editor`实例的内容时，该扩展将生成相应的 `<s>` HTML 标签。无论使用何种方法进行删除线操作，所有被划掉的文本都将规范化为 `<s>` HTML 标签。
:::

## 安装
```bash
npm install @tiptap/extension-strike
```

## 配置

### HTMLAttributes
在所呈现的 HTML 标签中添加的自定义 HTML 属性。

```js
Strike.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setStrike()
将文本标记为删除线。

```js
editor.commands.setStrike()
```

### toggleStrike()
切换删除线状态。

```js
editor.commands.toggleStrike()
```

### unsetStrike()
取消删除线标记。

```js
editor.commands.unsetStrike()
```

## 快捷键
| 命令           | Windows/Linux                   | MacOS                       |
| -------------- | ------------------------------- | --------------------------- |
| toggleStrike() | `Control`&nbsp;`Shift`&nbsp;`X` | `Cmd`&nbsp;`Shift`&nbsp;`X` |

## 源代码
[packages/extension-strike/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-strike/)

## 使用示例
https://embed.tiptap.dev/preview/Marks/Strike