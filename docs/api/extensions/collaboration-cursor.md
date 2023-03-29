# CollaborationCursor
[![Version](https://img.shields.io/npm/v/@tiptap/extension-collaboration-cursor.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-collaboration-cursor)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-collaboration-cursor.svg)](https://npmcharts.com/compare/@tiptap/extension-collaboration-cursor?minimal=true)

该扩展添加了有关所有连接用户的信息（例如他们的名称和指定的颜色），他们当前的光标位置和他们的文本选择（如果有）。

在多个浏览器窗口中打开此页面以进行测试。

:::pro 专业版扩展
在生产中使用此扩展时，我们请求您[sponsor我们的工作](/sponsor)。
:::

## 安装
```bash
npm install @tiptap/extension-collaboration-cursor
```

此扩展需要[`Collaboration`](/api/extensions/collaboration)扩展。

## 设置

### provider
一个 Y.js 网络提供者，例如[y-websocket](https://github.com/yjs/y-websocket)实例。

默认值：`null`

### user
当前用户的属性，假设有一个名称和颜色，但也可以与任何属性一起使用。这些值与所有其他连接的客户端同步。

默认值：`{ user: null，color: null }`

### render
光标的渲染函数，请参阅[扩展源代码](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-collaboration-cursor/)以获取示例。

## 命令

### updateUser()
传递一个对象，其中包含当前用户的更新属性。它期望有一个`name`和一个`color`，但您也可以添加附加字段。

```js
editor.commands.updateUser({
  name: 'John Doe',
  color: '#000000',
  avatar: 'https://unavatar.io/github/ueberdosis',
})
```

## 源代码
[packages/extension-collaboration-cursor/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-collaboration-cursor/)

## 用法
:::warning 公开
此编辑器的内容与其他用户共享。
:::
https://embed.tiptap.dev/preview/Extensions/CollaborationCursor?hideSource
https://embed.tiptap.dev/preview/Extensions/CollaborationCursor