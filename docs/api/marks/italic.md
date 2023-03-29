# 斜体文本

使用此扩展程序以呈现*斜体*文本。如果在编辑器的初始内容中传递了`<em>`、`<i>`标签或具有内联`style`属性设置`font-style:italic`的文本，则所有这些内容都将被相应地呈现。

而你只需输入`*一个星号*`或`_一个下划线_`，它就会像神奇般地转换成*斜体*文本。

::: warning 限制
该扩展程序在读取`Editor`实例的内容时将生成相应的`<em>`HTML标记。无论以哪种方法标记都将被标准化为`<em>`HTML标记的斜体文本。
:::

## 安装

```bash
npm install @tiptap/extension-italic
```

## 设置

### HTMLAttributes
应添加到呈现的HTML标记的自定义HTML属性。

```js
Italic.configure({
  HTMLAttributes: {
    class: 'my-custom-class',
  },
})
```
## 命令

### setItalic()
将文本标记为斜体。

```js
编辑器.commands.setItalic()
```

### toggleItalic()
切换斜体标记。

```js
编辑器.commands.toggleItalic()
```

### unsetItalic()
去除斜体标记。

```js
编辑器.commands.unsetItalic()
```

## 快捷键

| 命令         | Windows/Linux       | macOS              |
| ----------- | -------------------- | ------------------ |
| toggleItalic() | `Control`&nbsp;`I` | `Cmd`&nbsp;`I`   |

## 源代码
[packages/extension-italic/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-italic/)

## 使用方法
https：//embed.tiptap.dev/preview / Marks / Italic