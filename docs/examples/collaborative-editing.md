# 协作编辑

## 介绍
这个示例展示了如何使用 Tiptap 让多个用户实时协作编辑同一个文档。

它将所有客户端连接到一个 WebSocket 服务器，并借助 [Y.js](https://github.com/yjs/yjs) 的能力合并文档的更改。如果您想学习更多关于协作编辑的信息，请查看[我们的协作编辑指南](/guide/collaborative-editing)。

## 示例
:::warning 共享文档
请友好！此编辑器的内容与互联网上的其他用户共享。
:::

https://embed.tiptap.dev/preview/Examples/CollaborativeEditing

## 后端
如果你想知道在服务器上实现这个需要哪些魔法，这是演示的完整后端代码：

```js
import { Server } from '@hocuspocus/server'

const server = Server.configure({
  port: 80,
})

server.listen()
```