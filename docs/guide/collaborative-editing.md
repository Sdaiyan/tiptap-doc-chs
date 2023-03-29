# 协同编辑

## 介绍

实时协作、不同设备间的同步以及离线工作曾经是困难的。我们提供了一切你需要的，利用 [Y.js](https://github.com/yjs/yjs) 的强大功能来保持所有东西同步。以下指南将帮助你开始使用 Tiptap 进行协作编辑。别担心，生产级的设置不需要太多代码。

## [#](https://tiptap.dev/guide/collaborative-editing#the-video-course)视频课程

我们正在制作一个视频课程，教授有关在 Tiptap 中进行协作文本编辑所需的一切知识。赞助者可以在此处查看第一个视频：

观看视频： 使 Tiptap 具有协作功能 (06:46)

[![img](https://i.vimeocdn.com/filter/overlay?src0=https%3A%2F%2Fi.vimeocdn.com%2Fvideo%2F1284917566-6d875b34af836485a5195fda19c9f41e98f8a88d2fc1cb481_1280x720&src1=http%3A%2F%2Ff.vimeocdn.com%2Fp%2Fimages%2Fcrawler_play.png)](https://tiptap.dev/screencasts/collaborative-editing/make-tiptap-collaborative)

在这个视频中，我将添加 `Collaboration` 扩展到 Tiptap 中，向你展示如何将协作文本编辑功能添加到你的编辑器中。你将会学到为什么历史处理在协作编辑器中有所不同。

内容还没有通过网络同步，但我们将在额外的视频中介绍这一点。

## [#](https://tiptap.dev/guide/collaborative-editing#configure-the-editor)配置编辑器

Tiptap使用的底层schema是同步文档的良好基础。通过 [`Collaboration`](https://tiptap.dev/api/extensions/collaboration) 扩展，您可以告诉Tiptap使用 [Y.js](https://github.com/yjs/yjs) 跟踪文档的更改。

Y.js是一种无冲突复制数据类型实现，换句话说：它非常擅长合并更改。为了实现这一点，更改甚至不必按顺序进行。在离线时更改文档，并在设备重新联网时将其与其他更改合并，这是完全可行的。

某种程度上，所有客户端都需要在某个时刻交换文档修改。用于实现这一目的的最流行技术是 [WebRTC](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API) 和 [WebSockets](https://developer.mozilla.org/de/docs/Web/API/WebSocket)，因此让我们更详细地了解一下这些技术：

### [#](https://tiptap.dev/guide/collaborative-editing#web-rtc)WebRTC

WebRTC 仅使用服务器连接客户端。实际的数据流在客户端之间进行，而服务器对此一无所知，这是进行协作编辑的第一步非常好的方式。

首先，安装依赖项：

```sh
npm install @tiptap/extension-collaboration yjs y-webrtc y-prosemirror
```

现在，创建一个新的 Y 文档，并将其注册到 Tiptap：

```javascript
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Collaboration from '@tiptap/extension-collaboration'
import * as Y from 'yjs'
import { WebrtcProvider } from 'y-webrtc'

// 新的 Y 文档
const ydoc = new Y.Doc()
// 注册到 WebRTC 提供者
const provider = new WebrtcProvider('example-document', ydoc)

const editor = new Editor({
  extensions: [
    StarterKit.configure({
      // 协作扩展自带其自身的历史记录处理
      history: false,
    }),
    // 将文档注册到 Tiptap
    Collaboration.configure({
      document: ydoc,
    }),
  ],
})
```

这应该足以创建一个协作的 Tiptap 实例。非常神奇，不是吗？尝试在两个不同的浏览器中打开编辑器并进行更改，应该可以在不同的窗口之间同步更改。

那么这种神奇的工作原理是什么呢？所有客户端都需要相互连接，这是 *提供者* 的工作。 [WebRTC 提供者](https://github.com/yjs/y-webrtc) 是最简单的入门方式，因为它使用公共服务器直接将客户端连接在一起，但不用于同步实际的更改。但是，这有两个缺点。

1. 浏览器会拒绝连接太多的客户端。使用 Y.js 只需要间接连接所有客户端就足够了，但是在某些情况下甚至这也是不可能的。换句话说，在同一文档中同时有超过 100+ 并发客户端时，它不适用于大规模。
2. 你可能需要涉及一个服务器来持久化更改。但是，WebRTC 信令服务器（连接所有客户端）不会接收更改，因此不知道文档中有什么。

无论如何，如果你想深入了解，请前往 [Y WebRTC 存储库](https://github.com/yjs/y-webrtc)。

### [#](https://tiptap.dev/guide/collaborative-editing#web-socket)WebSocket（推荐）

对于大多数使用情况，WebSocket 提供者是推荐的选择。它非常灵活，可以很好地扩展。为了使它更容易使用，我们发布了 [Hocuspocus](https://hocuspocus.dev/) 作为 Tiptap 的官方后端。

对于客户端，示例几乎相同，只是提供者不同。首先，让我们安装依赖项：

```sh
npm install @tiptap/extension-collaboration @hocuspocus/provider y-prosemirror
```

然后，将 WebSocket 提供者与 Tiptap 注册：

```javascript
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Collaboration from '@tiptap/extension-collaboration'
import { HocuspocusProvider } from '@hocuspocus/provider'

// 设置 Hocuspocus WebSocket 提供者
const provider = new HocuspocusProvider({
  url: 'ws://127.0.0.1:1234',
  name: 'example-document',
})

const editor = new Editor({
  extensions: [
    StarterKit.configure({
      // 协作扩展带有自己的历史记录处理
      history: false,
    }),
    // 将文档与 Tiptap 注册
    Collaboration.configure({
      document: provider.document,
    }),
  ],
})
```

这个示例不是开箱即用的。正如你所看到的，它配置为连接到一个 WebSocket 服务器，该服务器在 `ws://127.0.0.1:1234` 下可用（WebSocket 协议 `ws://`，你的本地 IP `127.0.0.1` 和端口 `1234`）。你也需要设置它。

#### [#](https://tiptap.dev/guide/collaborative-editing#the-web-socket-backend)WebSocket 后端

为了使服务器部分尽可能简单，我们提供了一个名为 [Hocuspocus](http://hocuspocus.dev/) 的推荐服务器包。它是一个灵活的 Node.js 包，您可以用它来构建自己的自定义后端。

为了这个指南的目的，让我们只使用命令行界面，它可以在几秒钟内启动一个最小的服务器：

```sql

npx @hocuspocus/cli --port 1234 --sqlite
```

该命令会下载 Hocuspocus 命令行界面，启动一个在 1234 端口上监听的服务器，并将更改存储在内存中（一旦停止命令，它就会消失）。输出应该如下所示：

```yaml

Hocuspocus v1.0.0 running at:

> HTTP: http://127.0.0.1:1234
> WebSocket: ws://127.0.0.1:1234

Ready.
```

尝试在浏览器中打开 [http://127.0.0.1:1234](http://127.0.0.1:1234/)，如果一切正常，您应该会看到一个简单的文本“OK”。

返回到您的 Tiptap 编辑器，点击重新加载，它现在应该连接到 Hocuspocus WebSocket 服务器，并且更改应该与所有其他客户端同步。很神奇，不是吗？

### [#](https://tiptap.dev/guide/collaborative-editing#multiple-network-providers)多个网络提供商

你甚至可以组合多个提供商。虽然这不是必需的，但这样可以保持客户端的连接，即使一个连接 - 比如 WebSocket 服务器 - 暂时中断。以下是一个示例：

```javascript
new WebrtcProvider('example-document', ydoc)
new HocuspocusProvider({
  url: 'ws://127.0.0.1:1234',
  name: 'example-document',
  document: ydoc,
})
```

就是这样。

请记住，WebRTC 需要一个信令服务器来连接客户端。这个信令服务器不接收同步数据，但可以帮助客户端找到对方。如果你愿意，你可以[运行自己的信令服务器](https://github.com/yjs/y-webrtc#signaling)。否则，它将使用默认的 URL（包含在包中）。

### [#](https://tiptap.dev/guide/collaborative-editing#show-other-cursors)显示其他光标

为了让用户看到彼此的光标和文本选择，需要添加[`CollaborationCursor`](https://tiptap.dev/api/extensions/collaboration-cursor)扩展。

```javascript
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'
import Collaboration from '@tiptap/extension-collaboration'
import CollaborationCursor from '@tiptap/extension-collaboration-cursor'
import { HocuspocusProvider } from '@hocuspocus/provider'

// 设置 Hocuspocus WebSocket 提供商
const provider = new HocuspocusProvider({
  url: 'ws://127.0.0.1:1234',
  name: 'example-document',
})

const editor = new Editor({
  extensions: [
    StarterKit.configure({
      // Collaboration 扩展带有自己的历史记录处理
      history: false,
    }),
    Collaboration.configure({
      document: provider.document,
    }),
    // 注册协作光标扩展
    CollaborationCursor.configure({
      provider: provider,
      user: {
        name: 'Cyndi Lauper',
        color: '#f783ac',
      },
    }),
  ],
})
```

正如你所看到的，你可以为每个用户传递名称和颜色。查看[协作编辑示例](https://tiptap.dev/examples/collaborative-editing)，以查看更高级的示例。

### [#](https://tiptap.dev/guide/collaborative-editing#offline-support)离线支持

要将离线支持添加到你的协同编辑器中，基本上只需要一行代码，感谢神奇的[Y IndexedDB adapter](https://github.com/yjs/y-indexeddb)。安装它：

```sh
npm install y-indexeddb
```

然后将其与 Y 文档连接起来：

```javascript
import { Editor } from '@tiptap/core'
import Collaboration from '@tiptap/extension-collaboration'
import * as Y from 'yjs'
import { IndexeddbPersistence } from 'y-indexeddb'

const ydoc = new Y.Doc()

// 将 Y 文档存储在浏览器中
new IndexeddbPersistence('example-document', ydoc)

const editor = new Editor({
  extensions: [
    // …
    Collaboration.configure({
      document: ydoc,
    }),
  ],
})
```

然后，所有更改都将在浏览器中存储，即使你关闭了标签页、离线工作或在离线工作期间进行更改。下次你联网时，WebSocket provider 将尝试找到连接并最终同步更改。

是的，这就是魔法。正如前面提到的，这一切都基于神奇的 Y.js 框架。如果你正在使用它或我们的集成，你绝对应该[在 GitHub 上赞助 Kevin Jahns](https://github.com/dmonad)，他是 Y.js 的创造者。

## [#](https://tiptap.dev/guide/collaborative-editing#our-plug--play-collaboration-backend)我们的即插即用协作后端

我们的协作编辑后端[Hocuspocus](https://hocuspocus.dev/)处理同步，授权，持久化和扩展。我们来看一下一些常见的用例！

### [#](https://tiptap.dev/guide/collaborative-editing#the-document-name)文档名称

所有这里的例子中文档名称都是 `'example-document'`，但它可以是任何字符串。在实际应用程序中，您可能会添加实体的名称和实体的ID。以下是一个例子：

```javascript
const documentName = 'page.140'
```

在后端，您可以分割字符串以了解用户正在输入ID为140的页面，并相应地进行管理和授权。新文档会自动创建，无需告诉后端，只需将字符串传递给提供程序即可。

如果您想要使用一个 Y.js 文档同步多个字段，只需将不同的片段名称传递给协作扩展：

```javascript
// 一个用于字段的 Tiptap 实例
Collaboration.configure({
  document: ydoc,
  field: 'title',
})

// 另一个用于摘要的实例，两者在同一个 Y.js 文档中
Collaboration.configure({
  document: ydoc,
  field: 'summary',
})
```

如果您的设置更加复杂，例如有嵌套片段，则还可以传递原始的 Y.js 片段。`document` 和 `field` 将被忽略。

```css
// 一个原始的 Y.js 片段
Collaboration.configure({
  fragment: ydoc.getXmlFragment('custom'),
})
```

### [#](https://tiptap.dev/guide/collaborative-editing#authentication--authorization)身份验证和授权

使用 `onAuthenticate` 钩子，您可以检查客户端是否已验证身份和授权查看当前文档。在真实世界的应用中，这可能是对 API 的请求、数据库查询或其他内容。

当抛出错误（或拒绝返回的 Promise）时，与客户端的连接将被终止。如果客户端已经获得了授权和验证，您还可以返回上下文数据，这些数据可以在其他钩子中访问。但这不是必需的。

```javascript
import { Server } from '@hocuspocus/server'

const server = Server.configure({
  async onAuthenticate({ token }) {
    // 例如测试用户是否已验证
    if (token !== 'super-secret-token') {
      throw new Error('未经授权!')
    }

    // 您可以设置上下文数据以在其他钩子中使用它
    return {
      user: {
        id: 1234,
        name: 'John',
      },
    }
  },
})

server.listen()
```

## [#](https://tiptap.dev/guide/collaborative-editing#pitfalls)陷阱

### [#](https://tiptap.dev/guide/collaborative-editing#schema-updates)模式更新

Tiptap 对 [schema](https://tiptap.dev/api/schema) 非常严格，这意味着，如果您添加的内容不符合配置的 schema，它将被丢弃。当多个具有不同 schema 的客户端共享对文档的更改时，这可能会导致奇怪的行为。

假设您向应用程序添加了一个编辑器，而第一批使用它的人已经开始使用。他们都加载了 Tiptap 的所有默认扩展和一个只允许这些扩展的 schema。但是您想在下一个更新中添加任务列表，因此添加了该扩展并再次部署。

一个新用户打开您的应用程序，并拥有更新的 schema（包含任务列表），而其他所有用户仍然拥有旧的 schema（不包含任务列表）。新用户查看新添加的任务列表，并将其添加到文档中，以向该文档中的其他用户展示该功能。但是，然后，它会神奇地消失。发生了什么？

当一个用户添加一个新节点（或标记）时，该更改将同步到所有其他连接的客户端。其他连接的客户端将这些更改应用到编辑器中，而 Tiptap 严格执行，因此删除了新添加的节点，因为根据他们的（旧）schema 不允许。这些更改将同步到其他连接的客户端，糟糕的是，它在所有地方都被删除了。为避免这种情况，您有几个选择：

1. 永远不要更改 schema（不太好）。
2. 在部署新 schema 时强制客户端更新（困难）。
3. 跟踪 schema 版本并禁用对于具有过时 schema 的客户端的编辑器（取决于您的设置）。

我们计划提供功能来使这更容易。如果您有改进的想法，请与我们分享！