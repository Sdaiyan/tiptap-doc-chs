# 使用 Vue 进行 Node 视图

## 简介

如果你习惯于使用 Vue，那么使用原生 JavaScript 可能会感到比较复杂。好消息是：你也可以在 node 视图中使用常规的 Vue 组件。你只需要了解一些细节，接下来我们一步步讲解。

## [#](https://tiptap.dev/guide/node-views/vue#render-a-vue-component)渲染 Vue 组件

以下是在编辑器中渲染 Vue 组件的步骤：

1. [创建一个节点扩展](https://tiptap.dev/guide/custom-extensions)
2. 创建一个 Vue 组件
3. 将该组件传递给提供的 `VueNodeViewRenderer`
4. 使用 `addNodeView()` 注册该组件
5. [配置 Tiptap 来使用你的新节点扩展](https://tiptap.dev/guide/configuration)

以下是你的节点扩展的示例代码：

```javascript
import { Node } from '@tiptap/core'
import { VueNodeViewRenderer } from '@tiptap/vue-2'
import Component from './Component.vue'

export default Node.create({
  // 配置…

  addNodeView() {
    return VueNodeViewRenderer(Component)
  },
})
```

需要一些魔法才能使其正常工作，但不用担心，我们提供了一个包装组件，让你可以轻松入门。不要忘记将其添加到你的自定义 Vue 组件中，如下所示：

```php
<template>
  <node-view-wrapper>
    Vue 组件
  </node-view-wrapper>
</template>
```

明白了吗？我们来看看它的实际效果吧。你可以复制下面的示例进行尝试。

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/VueComponent?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer0" scrolling="no" style="overflow: hidden; height: 777px;"></iframe>

然而，该组件尚未与编辑器进行交互。是时候进行调试了。

## [#](https://tiptap.dev/guide/node-views/vue#access-node-attributes)访问节点属性

你在节点扩展中使用的 `VueNodeViewRenderer` 会将几个非常有用的 props 传递给你的自定义 Vue 组件。其中之一是 `node` prop。将以下代码添加到你的 Vue 组件中，以直接访问节点：

```yaml
props: {
  node: {
    type: Object,
    required: true,
  },
},
```

这使得你可以在你的 Vue 组件中访问节点属性。比如说，假设你已经 [添加了一个名为 `count` 的属性](https://tiptap.dev/guide/custom-extensions#attributes) 到你的节点扩展中（就像我们在上面的示例中所做的那样），你可以像这样访问它：

```kotlin
this.node.attrs.count
```

## [#](https://tiptap.dev/guide/node-views/vue#update-node-attributes)更新节点属性

你甚至可以通过传递给你的组件的 `updateAttributes` prop 来更新节点属性。只需将以下代码添加到你的组件中：

```yaml
props: {
  updateAttributes: {
    type: Function,
    required: true,
  },
},
```

将包含更新属性的对象传递给函数：

```kotlin
this.updateAttributes({
  count: this.node.attrs.count + 1,
})
```

是的，所有这些都是响应式的。这是一种相当无缝的通信方式，不是吗？

## [#](https://tiptap.dev/guide/node-views/vue#adding-a-content-editable)添加可编辑内容

还有另一个组件叫做`NodeViewContent`，它可以帮助您向节点视图添加可编辑内容。以下是一个例子：

```php
<template>
  <node-view-wrapper class="dom">
    <node-view-content class="content-dom" />
  </node-view-wrapper>
</template>

<script>
import { NodeViewWrapper, NodeViewContent } from '@tiptap/vue-2'

export default {
  components: {
    NodeViewWrapper,
    NodeViewContent,
  },
}
</script>
```

您不需要添加这些`class`属性，可以随意删除它们或传递其他类名。在以下示例中尝试：

<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/VueComponentContent?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer1" scrolling="no" style="overflow: hidden; height: 777px;"></iframe>

请记住，此内容是由Tiptap呈现的。这意味着您需要告诉它哪些内容是允许的，例如在您的节点扩展中使用`content: 'inline*'`（这是我们在上面的示例中使用的方法）。

`NodeViewWrapper`和`NodeViewContent`组件呈现`<div>`HTML标记（对于内联节点为`<span>`），但您可以更改它。例如，`<node-view-content as="p">`应该呈现一个段落。但是有一个限制：该标记在运行时不能更改。

## [#](https://tiptap.dev/guide/node-views/vue#all-available-props)可用的所有属性

对于高级用例，我们向组件传递了更多的属性。

### [#](https://tiptap.dev/guide/node-views/vue#editor)editor

编辑器实例。

### [#](https://tiptap.dev/guide/node-views/vue#node)node

访问当前节点。

### [#](https://tiptap.dev/guide/node-views/vue#decorations)decorations

修饰数组。

### [#](https://tiptap.dev/guide/node-views/vue#selected)selected

当当前节点视图存在`NodeSelection`时为 `true`。

### [#](https://tiptap.dev/guide/node-views/vue#extension)extension

访问节点扩展，例如获取选项。

### [#](https://tiptap.dev/guide/node-views/vue#get-pos)getPos()

获取当前节点的文档位置。

### [#](https://tiptap.dev/guide/node-views/vue#update-attributes)updateAttributes()

更新当前节点的属性。

### [#](https://tiptap.dev/guide/node-views/vue#delete-node)deleteNode()

删除当前节点。

下面是所有属性的完整列表：

```php
<template>
  <node-view-wrapper />
</template>

<script>
import { NodeViewWrapper } from '@tiptap/vue-2'

export default {
  components: {
    NodeViewWrapper,
  },

  props: {
    // 编辑器实例
    editor: {
      type: Object,
    },

    // 当前节点
    node: {
      type: Object,
    },

    // 修饰数组
    decorations: {
      type: Array,
    },

    // 当前节点视图存在`NodeSelection`时为 `true`
    selected: {
      type: Boolean,
    },

    // 访问节点扩展，例如获取选项
    extension: {
      type: Object,
    },

    // 获取当前节点的文档位置
    getPos: {
      type: Function,
    },

    // 更新当前节点的属性
    updateAttributes: {
      type: Function,
    },

    // 删除当前节点
    deleteNode: {
      type: Function,
    },
  },
}
</script>
```

如果你只是想要所有属性（和 TypeScript 支持），可以像这样导入所有属性：

```javascript
// Vue 3
import { defineComponent } from 'vue'
import { nodeViewProps } from '@tiptap/vue-3'
export default defineComponent({
  props: nodeViewProps,
})

// Vue 2
import Vue from 'vue'
import { nodeViewProps } from '@tiptap/vue-2'
export default Vue.extend({
  props: nodeViewProps,
})
```

## [#](https://tiptap.dev/guide/node-views/vue#dragging)拖拽

要使你的节点视图可拖动，在扩展中设置 `draggable: true`，并在应作为拖动手柄的 DOM 元素中添加 `data-drag-handle`。



<iframe src="https://embed.tiptap.dev/preview/GuideNodeViews/DragHandle?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0" id="iFrameResizer2" scrolling="no" style="overflow: hidden; height: 1009px;"></iframe>

