# 提及

https://embed.tiptap.dev/preview/Examples/Community

在社交网络或协作工具中，提及特定用户是很常见的需求，因此在一个编辑器中支持提及也非常的必要。Tiptap 支持使用 `@` 符号提及用户的功能，这个功能可以在任何需要输入文本的地方使用。在输入 `@` 符号后，编辑器会弹出一个提及面板，用户可以在面板中选择要提及的用户。被提及的用户在编辑器中会被标记出来，当鼠标滑过这个标记时，会显示该用户的详细信息。

![](https://tiptap.s3.amazonaws.com/api/v1/examples/community-mentions.png)

## 安装

引入 Tiptap 之后，在需要使用提及功能的地方，引入提及插件：

```js
import { Mention } from '@tiptap/extension-mention'
```

接下来，通过 `editor.use` 使用该插件：

```js
editor.use(Mention, {
  // options
})
```

## 选项

Mention 插件支持以下选项：

| 名称 | 类型 | 默认值 | 描述 |
| --- | --- | --- | --- |
| `HTMLAttributes` | `object` | `{}` | 传递给渲染所使用的虚拟节点的 HTML 属性 |
| `suggestions` | `array` | `[]` | 一个数组，包含需要提供用户选择的所有可选项。 |

例如：

```js
editor.use(Mention, {
  HTMLAttributes: {
    class: 'mention',
  },
  suggestions: [
    { id: 1, name: 'John Doe', handle: 'johndoe' },
    { id: 2, name: 'Jane Doe', handle: 'janedoe' },
  ],
})
```