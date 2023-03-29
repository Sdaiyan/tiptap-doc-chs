# 访问 ProseMirror 内部

Tiptap 是基于 ProseMirror 构建的，ProseMirror 具有非常强大的 API。为了访问它，我们提供了 `@tiptap/pm` 包。该包提供了所有重要的 ProseMirror 包，如 `prosemirror-state`、`prosemirror-view` 或 `prosemirror-model`。使用该包进行自定义开发可确保您始终具有 Tiptap 使用的相同版本的 ProseMirror。这样，我们可以确保 Tiptap 和所有扩展与彼此兼容，并防止版本冲突。另外一个好处是，您不需要手动安装所有的 ProseMirror 包，特别是如果您没有使用支持自动对等依赖解决的 npm 或其他包管理器。

安装：

```sh
npm i @tiptap/pm
```

安装后，您可以像这样访问所有内部的 ProseMirror 包：

```javascript
// 此示例从 ProseMirror state 包中加载 EditorState 类
import { EditorState } from '@tiptap/pm/state'
```

可用的包括以下内容：

- `@tiptap/pm/changeset`
- `@tiptap/pm/collab`
- `@tiptap/pm/commands`
- `@tiptap/pm/dropcursor`
- `@tiptap/pm/gapcursor`
- `@tiptap/pm/history`
- `@tiptap/pm/inputrules`
- `@tiptap/pm/keymap`
- `@tiptap/pm/markdown`
- `@tiptap/pm/menu`
- `@tiptap/pm/model`
- `@tiptap/pm/schema-basic`
- `@tiptap/pm/schema-list`
- `@tiptap/pm/state`
- `@tiptap/pm/tables`
- `@tiptap/pm/trailing-node`
- `@tiptap/pm/transform`
- `@tiptap/pm/view`

您可以在 [ProseMirror 文档](https://prosemirror.net/docs/ref) 中了解更多关于这些库的信息。