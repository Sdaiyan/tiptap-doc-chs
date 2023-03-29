# 使用 JavaScript 的节点视图

## 介绍

如果你习惯不使用 Vue 或 React 等框架，使用这些框架可能会感到过于复杂。好消息是，你可以在节点视图中使用原生 JavaScript。只需要了解一点点就行，我们一步一步来看。

## [#](https://tiptap.dev/guide/node-views/js#render-a-node-view-with-java-script)使用 JavaScript 渲染节点视图

以下是在编辑器中渲染节点视图所需的步骤：

1. [创建一个节点扩展](https://tiptap.dev/guide/custom-extensions)
2. 使用 `addNodeView()` 注册一个新的节点视图
3. 编写渲染函数
4. [配置 Tiptap 使用你的新节点扩展](https://tiptap.dev/guide/configuration)

以下是你的节点扩展的示例代码：

```javascript
import { Node } from '@tiptap/core'
import Component from './Component.vue'

export default Node.create({
  // configuration …

  addNodeView() {
    return ({ editor, node, getPos, HTMLAttributes, decorations, extension }) => {
      const dom = document.createElement('div')

      dom.innerHTML = 'Hello, I’m a node view!'

      return {
        dom,
      }
    }
  },
})
```

明白了吗？接下来我们来看看它的实际应用。你可以复制下面的示例代码开始尝试。

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/JavaScript?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0"></iframe>

这个节点视图甚至可以与编辑器交互。现在是时候看看它是如何被连接起来的了。

## [#](https://tiptap.dev/guide/node-views/js#access-node-attributes)访问节点属性

编辑器会向你的渲染函数传递一些有用的内容，其中之一是`node`属性。这个属性使你能够在节点视图中访问节点属性。假设你已经[添加了一个名为`count`的属性](https://tiptap.dev/guide/custom-extensions#attributes)到你的节点扩展中，你可以像这样访问该属性：

```javascript
addNodeView() {
  return ({ node }) => {
    console.log(node.attrs.count)

    // …
  }
}
```

## [#](https://tiptap.dev/guide/node-views/js#update-node-attributes)更新节点属性

你甚至可以从节点视图中更新节点属性，使用传递给你渲染函数的`getPos`属性。用包含更新后属性的对象分派一个新的事务：

```javascript
addNodeView() {
  return ({ editor, node, getPos }) => {
    const { view } = editor

    // 创建一个按钮...
    const button = document.createElement('button')
    button.innerHTML = `This button has been clicked ${node.attrs.count} times.`

    // ...当它被点击时...
    button.addEventListener('click', () => {
      if (typeof getPos === 'function') {
        // ...分派一个事务，针对文档中当前位置...
        view.dispatch(view.state.tr.setNodeMarkup(getPos(), undefined, {
          count: node.attrs.count + 1,
        }))

        // ...并把焦点设回到编辑器。
        editor.commands.focus()
      }
    })

    // ...
  }
}
```

这看起来有点复杂？如果你的项目中已经有[React](https://tiptap.dev/guide/node-views/react)或[Vue](https://tiptap.dev/guide/node-views/vue)之一，考虑使用它们，这样会更容易一些。

## [#](https://tiptap.dev/guide/node-views/js#adding-a-content-editable)添加可编辑内容

要向节点视图添加可编辑内容，您需要传递一个 `contentDOM`，一个用于内容的容器元素。下面是一个简化版本的节点视图，其中包含不可编辑和可编辑的文本内容：

```javascript
// 创建节点视图的容器
const dom = document.createElement('div')

// 将包含文本的其他元素的 `contentEditable` 属性设置为 false
const label = document.createElement('span')
label.innerHTML = '节点视图'
label.contentEditable = false

// 创建内容的容器
const content = document.createElement('div')

// 将所有元素附加到节点视图容器上
dom.append(label, content)

return {
  // 传递节点视图容器...
  dom,
  // ... 和内容容器：
  contentDOM: content,
}
```

明白了吗？只要返回一个节点视图的容器和另一个用于内容的容器，您就可以做任何您想做的事情。下面是上面示例的实现效果：

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/JavaScriptContent?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0"></iframe>

请记住，这些内容是由 Tiptap 渲染的。这意味着您需要告诉 Tiptap 允许使用何种类型的内容，例如在您的节点扩展中使用 `content: 'inline*'`（这就是我们在上面的示例中使用的方法）。