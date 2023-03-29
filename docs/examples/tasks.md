# 任务

https://embed.tiptap.dev/preview/Examples/Tasks

## 概述

这个例子展示了如何使用 tiptap 编辑一个有任务列表的文档。每个任务可以被勾选或取消勾选。

## 示例

在下面的代码块中，我们创建一个任务列表，并编写了一个 `Task` 组件来呈现任务列表的每个项目：

```vue
<template>
  <editor-content class="task-list">
    <ul>
      <li v-for="(node, i) in nodes">
        <task :node="node" :index="i" @toggle="$emit('toggle', i)" />
      </li>
    </ul>
  </editor-content>
</template>

<script>
import { Node } from '@tiptap/core'

export default {
  props: {
    nodes: {
      type: Array,
      required: true,
    },
  },

  components: {
    'task': {
      props: {
        node: {
          type: Object,
          required: true,
        },

        index: {
          type: Number,
          required: true,
        },
      },

      computed: {
        checked() {
          return this.node.attrs.completed
        },

        label() {
          return this.node.textContent
        },
      },

      methods: {
        toggle() {
          this.$emit('toggle')
        },
      },

      render(h) {
        return h('div', [
          h('input', {
            attrs: {
              type: 'checkbox',
              checked: this.checked,
            },
            on: {
              change: this.toggle,
            },
          }),
          h('span', this.label),
        ])
      },
    },
  },
}
</script>

<style>
.task-list {
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  li {
    display: flex;

    & + li {
      margin-top: 10px;
    }
  }

  input[type=checkbox] {
    margin-right: 10px;
  }
}
</style>
```

这里，我们声明了一个 `Task` 组件来渲染我们的任务列表。该组件依赖于一个名为 `node` 的 prop，它包含要呈现的任务的实际内容。我们从 `textContent` 中赋值给 `label` 的计算属性，以此来设置任务的文本标签。

我们还定义了一个 `checked` 计算属性，它通过读取 `completed` 节点属性（该属性表示任务是否已完成）来确定任务是否已完成。然后我们把它传递给复选框的 `checked` 属性。

我们为复选框的 `change` 事件定义了一个 `toggle` 方法，这个方法会通过 `$emit` 将 `toggle` 事件传递出组件。

最后，我们将渲染任务列表的每个项目的任务组件包括在一个 `v-for` 循环中，以便为每个节点渲染一个任务项。

## 用法

首先，我们将需要添加的节点类型和属性定义添加到我们的编辑器实例中：

```js
new Editor({
  // ...
  content: `
    <ul>
      <li>
        <task-list>
          <task completed="false">Task 1</task>
          <task completed="true">Task 2</task>
        </task-list>
      </li>
    </ul>
  `,
  extensions: [
    TaskList.configure({
      // ...
    }),
  ],
})
```

然后，我们可以通过监听 `toggle` 事件来更改节点属性：

```js
new Editor({
  // ...
  onUpdate({ editor }) {
    const tasks = editor.getNodes().filter(node => node.type.name === 'task')

    tasks.forEach((task, index) => {
      task.attrs.completed = this.tasks[index].completed
    })
  },
  data() {
    return {
      tasks: [
        { label: 'Task 1', completed: false },
        { label: 'Task 2', completed: true },
      ],
    }
  },
  methods: {
    onToggle(index) {
      this.tasks[index].completed = !this.tasks[index].completed
    },
  },
  content: `
    <ul>
      <li>
        <task-list :nodes="tasks" @toggle="onToggle" />
      </li>
    </ul>
  `,
  extensions: [
    TaskList.configure({
      // ...
    }),
  ],
})
```

在 `update` 生命周期钩子中，我们遍历所有节点，寻找名称为 `task` 的节点类型，并根据 `tasks` 数组中的相应完成状态更新它们的属性。在 `data()` 中，我们初始化 `tasks` 数组以包含要包含在任务列表中的每个任务，以及每个任务的初始化状态。当某个任务的复选框被勾选或未勾选时，`onToggle()` 方法会被触发。这将导致更改 `tasks` 数组中相应任务的完成状态。

最后，我们将渲染 `task-list` 组件。我们将 `nodes` prop 设置为 `tasks` 数组，并在 `toggle` 事件上监听，以便在完成任务时更改 `tasks` 数组的状态。