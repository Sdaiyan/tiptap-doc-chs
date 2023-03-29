# Bold

使用此扩展可以让文本以**粗体**展现。如果在编辑器的初始内容中传递`<strong>`、`<b>`标签或具有内联`style`属性并设置了`font-weight`CSS规则的文本，它们都将被相应地渲染。

输入`**两个星号**`或`__两条下划线__`，它会在您输入时自动变为**粗体**文本。

::: 警告 限制
当阅读`Editor`实例的内容时，扩展将生成相应的`< strong>` HTML标记。所有标记为粗体的文本，无论采用何种方法，都将被规范化为`<strong>`HTML标记。
:::

## 安装

```bash
npm install @tiptap/extension-bold
```

## 设置

### HTMLAttributes
应添加到呈现的 HTML 标记的自定义 HTML 特性。

```js
Bold.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```

## 命令

### setBold()
将文本标记为粗体。

```js
editor.commands.setBold()
```

### toggleBold()
切换粗体标记。

```js
editor.commands.toggleBold()
```

### unsetBold()
删除粗体标记。

```js
editor.commands.unsetBold()
```

## 键盘快捷方式

| 命令        | Windows/Linux      | macOS          |
| ------------ | ------------------ | -------------- |
| toggleBold() | `Control`&nbsp;`B` | `Cmd`&nbsp;`B` |

## 源代码

[packages/extension-bold/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bold/)

## 使用

https://embed.tiptap.dev/preview/Marks/Bold