# 交互式节点视图

## 简介

节点视图是切片面包之后最好的东西，至少对于喜欢自定义（和面包）的人来说是这样。使用节点视图，你可以向编辑器添加交互式节点。它可以是任何东西，只要你能用 JavaScript 写出来，你就可以在你的编辑器中使用它。

节点视图非常适合改进编辑器体验，但也可以在 Tiptap 的只读实例中使用。由于节点视图与 HTML 输出无关，因此你可以完全控制编辑器体验和输出。

## [#](https://tiptap.dev/guide/node-views#different-types-of-node-views)不同类型的节点视图

根据你想构建什么，节点视图的工作方式可能有所不同，也可能具有其特定的功能和缺陷。主要问题是：你的自定义节点应该长什么样？

### [#](https://tiptap.dev/guide/node-views#editable-text)可编辑文本

是的，节点视图可以具有可编辑文本，就像普通节点一样。这很简单。光标的行为将与普通节点完全相同。现有命令与这些节点非常兼容。

```html
<div class="Prosemirror" contenteditable="true">
  <p>text</p>
  <node-view>text</node-view>
  <p>text</p>
</div>
```

这就是 [`TaskItem`](https://tiptap.dev/api/nodes/task-item) 节点的工作方式。

### [#](https://tiptap.dev/guide/node-views#non-editable-text)不可编辑文本

节点也可以具有不可编辑的文本。光标无法进入这些文本，但你也不想这样做。

Tiptap 默认为这些添加了 `contenteditable="false"`。

```html
<div class="Prosemirror" contenteditable="true">
  <p>text</p>
  <node-view contenteditable="false">text</node-view>
  <p>text</p>
</div>
```

这就是你可以呈现出提到（mentions）的方式，因为它们不应该是可编辑的。用户可以添加或删除它们，但不能删除单个字符。

Statamic 在其 Bard 编辑器中使用这些内容，将 Tiptap 中的复杂模块呈现为可以拥有自己的文本输入的模块。

### [#](https://tiptap.dev/guide/node-views#mixed-content)混合内容

您甚至可以混合非可编辑和可编辑的文本。这很适合构建复杂的内容，并且在可编辑的内容中仍然可以使用加粗和斜体等标记。

**但是**，如果您的节点视图中存在其他具有非可编辑文本的元素，则光标可能会跳转到那里。您可以通过在节点视图的特定部分手动添加 `contenteditable="false"` 来改进它。

```html
<div class="Prosemirror" contenteditable="true">
  <p>text</p>
  <node-view>
    <div contenteditable="false">
      non-editable text
    </div>
    <div>
      editable text
    </div>
  </node-view>
  <p>text</p>
</div>
```

## [#](https://tiptap.dev/guide/node-views#markup)标记

但是，如果您[访问编辑器内容](https://tiptap.dev/guide/output)呢？如果您使用的是 HTML，您需要告诉 Tiptap 如何序列化您的节点。

编辑器**不会**导出呈现的 JavaScript 节点，对于很多用例，您也不希望这样做。

假设您有一个节点视图，允许用户添加视频播放器并配置外观（自动播放、控件等）。您希望在编辑器中完成这个界面，而不是在编辑器的输出中完成。编辑器的输出可能只需要包含视频播放器。

我知道，我知道，这并不容易。只要记住，您完全控制编辑器内部的呈现和输出。

## 如果您存储 JSON 呢？

这不适用于 JSON。在 JSON 中，一切都存储为对象。没有必要配置与 JSON 的“转换”。

### [#](https://tiptap.dev/guide/node-views#render-html)呈现 HTML

好的，您已经使用交互式节点视图设置了节点，现在您想控制输出。即使您的节点视图非常复杂，呈现的 HTML 也可以很简单：

```html
renderHTML({ HTMLAttributes }) {
  return ['my-custom-node', mergeAttributes(HTMLAttributes)]
},

// Output: <my-custom-node count="1"></my-custom-node>
```

确保它是可以区分的，以便从 HTML 中更轻松地还原内容。如果您只需要一些通用的标记，比如一个 `<div>`，考虑添加一个 `data-type="my-custom-node"`。

### [#](https://tiptap.dev/guide/node-views#parse-html)解析 HTML

同样的技巧也可以用于还原内容。你可以配置期望的标记，这可以是与节点视图标记完全无关的东西。它只需要包含您想要还原的所有信息即可。

如果您通过 [`addAttributes`](https://tiptap.dev/guide/custom-extensions#attributes) 注册了属性，则它们将自动还原。

```javascript
// 输入: <my-custom-node count="1"></my-custom-node>

parseHTML() {
  return [{
    tag: 'my-custom-node',
  }]
},
```

### [#](https://tiptap.dev/guide/node-views#render-java-scriptvuereact)呈现 JavaScript/Vue/React

但是如果您想呈现您的实际 JavaScript/Vue/React 代码怎么办？考虑使用 Tiptap 呈现您的输出。只需将编辑器设置为 `editable: false`，就没有人会注意到您正在使用编辑器来呈现内容。 :-)