# Placeholder（占位符）

这个插件可以提供占位符的支持，以小提示的形式向用户传达他们应该输入些什么。另外，你还可以进行一些定制。

## 安装
```bash
npm install @tiptap/extension-placeholder
```

### 额外设置
占位符是通过 CSS 显示出来的。

**仅在空编辑器的第一行显示占位符**
```css
.ProseMirror p.is-editor-empty:first-child::before {
  color: #adb5bd;
  content: attr(data-placeholder);
  float: left;
  height: 0;
  pointer-events: none;
}
```
**在每一行都显示占位符**
```css
.ProseMirror p.is-empty::before {
  color: #adb5bd;
  content: attr(data-placeholder);
  float: left;
  height: 0;
  pointer-events: none;
}
```


## 设置

### emptyEditorClass
如果编辑器为空，则添加的 CSS 类名。

默认值：`'is-editor-empty'`

```js
Placeholder.configure({
  emptyEditorClass: 'is-editor-empty',
})
```

### emptyNodeClass
如果节点为空，则添加的 CSS 类名。

默认值：`'is-empty'`

```js
Placeholder.configure({
  emptyNodeClass: 'my-custom-is-empty-class',
})
```

### placeholder
添加为 `data-placeholder` 属性的占位符文本。

默认为: `'Write something …'`

```js
Placeholder.configure({
  placeholder: 'My Custom Placeholder',
})
```

你甚至可以使用函数根据节点添加不同的占位符：

```js
Placeholder.configure({
  placeholder: ({ node }) => {
    if (node.type.name === 'heading') {
      return 'What’s the title?'
    }

    return 'Can you add some further context?'
  },
})
```

### showOnlyWhenEditable
仅在编辑器可编辑时显示装饰。

默认：`true`

```js
Placeholder.configure({
  showOnlyWhenEditable: false,
})
```

### showOnlyCurrent
仅在当前选定的节点中显示装饰。

默认：`true`

```js
Placeholder.configure({
  showOnlyCurrent: false
})
```

### includeChildren
同时显示嵌套节点的装饰。

默认值：`false`

```js
Placeholder.configure({
  includeChildren: true
})
```


## 源代码
[packages/extension-placeholder/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-placeholder/)

## 用法
https://embed.tiptap.dev/preview/Extensions/Placeholder