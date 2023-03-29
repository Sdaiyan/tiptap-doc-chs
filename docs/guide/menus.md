# 创建菜单

## 介绍

Tiptap 很原始，但这是好事。您可以完全控制其外观。

当我们说完全控制时，我们是指您可以（并且必须）自行构建菜单。我们会帮助您将所有内容连线起来。

## 菜单

编辑器提供了流畅的 API 来触发命令并添加活动状态。您可以使用任何标记。为了使菜单的定位更容易，我们提供了一些工具和组件。让我们一一介绍最典型的用例。

### 固定菜单

固定菜单，例如在编辑器顶部，可以是任何内容。我们不提供这种菜单。只需添加一个带有几个`<button>`的`<div>`即可。这些按钮如何触发[命令](https://tiptap.dev/api/commands) 在下面进行了[解释](https://tiptap.dev/guide/menus#buttons)。

### 气泡菜单

[气泡菜单](https://tiptap.dev/api/extensions/bubble-menu)会在选择文本时出现。标记和样式完全由您掌控。

<iframe src="https://embed.tiptap.dev/preview/Extensions/BubbleMenu?inline=false&amp;hideSource=true" width="100%" height="0" frameborder="0" id="iFrameResizer1" scrolling="no" style="overflow: hidden; height: 230px;"></iframe>

### 浮动菜单

[浮动菜单](https://tiptap.dev/api/extensions/floating-menu)在空行中出现。标记和样式完全由您掌控。

<iframe src="https://embed.tiptap.dev/preview/Extensions/FloatingMenu?inline=false&amp;hideSource=true" width="100%" height="0" frameborder="0" id="iFrameResizer0" scrolling="no" style="overflow: hidden; height: 230px;"></iframe>

### 斜杠命令(正在开发中)

它还不是官方扩展，但[有一个实验](https://tiptap.dev/experiments/commands) 可以用来添加我们所谓的斜杠命令。它允许您以 `/` 开始新行，并弹出一个窗口来选择应添加哪个节点。

## 按钮

好了，你已经有了你的菜单。但是如何将它们与功能联系起来呢？

### [#](https://tiptap.dev/guide/menus#commands)命令

您已经运行了编辑器并希望添加您的第一个按钮。您需要一个带有单击处理程序的`<button>` HTML 标记。根据您的设置，它可能类似于以下示例：

```jsx
<button onclick="editor.chain().focus().toggleBold().run()">
  Bold
</button>
```

哦，这是一个很长的命令，对吧？实际上，这是一个[命令链](https://tiptap.dev/api/commands#chain-commands)。我们逐个解释一下：

```jsx
editor.chain().focus().toggleBold().run()
```

1. `editor` 应该是一个 Tiptap 实例，
2. `chain()` 用于告诉编辑器您想要执行多个命令，
3. `focus()` 将焦点设置回编辑器，
4. `toggleBold()` 标记所选文本为粗体，如果已经应用则将粗体标记从文本选择中删除，
5. `run()` 将执行链。

换句话说：这将是文本编辑器的典型**粗体**按钮。

可用的命令取决于您已向编辑器注册了哪些扩展。大多数扩展都配有`set...()`、`unset...()`和`toggle...()`命令。阅读扩展文档以了解实际可用内容，或浏览您的代码编辑器的自动完成。

### [#](https://tiptap.dev/guide/menus#keep-the-focus)保持焦点

您已经在上面的示例中看到了`focus()`命令。当您单击按钮时，浏览器将聚焦于该 DOM 元素，而编辑器将失去焦点。您可能希望将`focus()`添加到所有菜单按钮中，以确保不会中断用户的书写流程。

### [#](https://tiptap.dev/guide/menus#the-active-state)活动状态

编辑器提供了一个`isActive()`方法，用于检查所选文本是否已应用。在 Vue.js 中，您可以使用该函数来切换 CSS 类，如下所示：

```vue
<button :class="{ 'is-active': editor.isActive('bold') }" @click="editor.chain().focus().toggleBold().run()">
  Bold
</button>
```

这将相应地切换`.is-active`类，并适用于节点和标记。您甚至可以检查特定属性。这是使用[`Highlight`](https://tiptap.dev/api/marks/highlight)标记的示例，它忽略了不同的属性：

```javascript
editor.isActive('highlight')
```

以下是比较给定属性的示例：

```
editor.isActive('highlight', { color: '#ffa8a8' })
```

甚至支持正则表达式：

```javascript
editor.isActive('textStyle', { color: /.*/ })
```

您甚至可以检查节点和标记，但仅检查属性。以下是使用 [`TextAlign`](https://tiptap.dev/api/extensions/text-align) 扩展的示例：

```javascript
editor.isActive({ textAlign: 'right' })
```

如果您的选择跨越多个节点或标记，或者只有选择的一部分具有标记，则 `isActive()` 将返回 `false` 并指示没有激活状态。这正是预期的，因为它允许人们立即将新节点或标记应用于该选择。

## [#](https://tiptap.dev/guide/menus#user-experience)用户体验

设计出色的用户体验时应考虑一些因素。

### [#](https://tiptap.dev/guide/menus#accessibility)可访问性

- 确保用户可以使用键盘导航菜单
- 使用正确的 [title 属性](https://developer.mozilla.org/de/docs/Web/HTML/Global_attributes/title)
- 使用正确的 [aria 属性](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/WAI-ARIA_basics)
- 列出可用的键盘快捷键

## 不完整

这个部分还需要一些工作。您知道构建编辑器菜单时还需要考虑什么吗？请在 [GitHub](https://github.com/ueberdosis/tiptap) 上告诉我们或向我们发送电子邮件到 [humans@tiptap.dev](mailto:humans@tiptap.dev)！

### [#](https://tiptap.dev/guide/menus#icons)图标

大多数编辑器菜单都使用图标来表示它们的按钮。在我们的一些演示中，我们使用开源图标集 [Remix Icon](https://remixicon.com/)，它是免费使用的。但是您完全可以选择其他图标。以下是您可以考虑的一些图标集：

- [Remix Icon](https://remixicon.com/#editor)
- [Font Awesome](https://fontawesome.com/icons?c=editors)
- [UI icons](https://www.ibm.com/design/language/iconography/ui-icons/library/)