---
title: Vue.js 3 富文本编辑器
tableOfContents: true
---

# Vue.js 3

## 介绍
以下教程描述了如何将 Tiptap 与您的 [Vue](https://vuejs.org/) CLI 项目集成。

## 要求
* 在您的计算机上安装 [Node](https://nodejs.org/en/download/)
* 在您的计算机上安装 [Vue CLI](https://cli.vuejs.org/)
* 熟悉 [Vue](https://v3.vuejs.org/guide/introduction.html)

## 1. 创建项目 (可选)
如果您已经有一个现有的 Vue 项目，那也可以。跳过此步骤，继续进行下一步。

为了本教程的目的，让我们从一个名为 `my-tiptap-project` 的新 Vue 项目开始。Vue CLI 将设置我们所需要的一切，只需选择 Vue 3 模板。

```bash
# 创建项目
vue create my-tiptap-project

# 切换目录
cd my-tiptap-project
```

## 2. 安装依赖
好了，够繁琐的样板工作了。让我们终于安装 Tiptap！对于以下示例，您需要 `@tiptap/vue-3` 包，`@tiptap/pm` (ProseMirror 库) 以及包括最常用的扩展的 `@tiptap/starter-kit`。

```bash
npm install @tiptap/vue-3 @tiptap/pm @tiptap/starter-kit
```

如果您按照第 1 步和第 2 步操作，现在可以使用 `npm run serve` 启动项目，并在您喜欢的浏览器中打开 [http://localhost:8080](http://localhost:8080)。如果您正在使用现有的项目，则可能会有所不同。

## 3. 创建新组件
要真正开始使用 Tiptap，您需要向应用程序中添加一个新组件。我们称之为 `Tiptap`，并将以下示例代码放入 `components/Tiptap.vue` 中。

这是使用 Vue 快速启动 Tiptap 的最快方法。它将为您提供一个非常基本的 Tiptap 版本，没有任何按钮。别担心，您很快就能添加更多功能。

```html
<template>
  <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null,
    }
  },

  mounted() {
    this.editor = new Editor({
      content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
      extensions: [
        StarterKit,
      ],
    })
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>
```

或者，您可以使用 `useEditor` 方法使用组合 API。

```html
<template>
  <editor-content :editor="editor" />
</template>

<script>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

export default {
  components: {
    EditorContent,
  },

  setup() {
    const editor = useEditor({
      content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
      extensions: [
        StarterKit,
      ],
    })

    return { editor }
  },
}
</script>
```

或者使用新的 [`<script setup>` 语法](https://v3.vuejs.org/api/sfc-script-setup.html)。

```html
<template>
  <editor-content :editor="editor" />
</template>

<script setup>
import { useEditor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

const editor = useEditor({
  content: '<p>I’m running Tiptap with Vue.js. 🎉</p>',
  extensions: [
    StarterKit,
  ],
})
</script>
```

## 4. 添加到应用中
现在，让我们使用以下示例代码替换 `src/App.vue` 的内容，以在应用程序中使用新的 `Tiptap` 组件。

```html
<template>
  <div id="app">
    <tiptap />
  </div>
</template>

<script>
import Tiptap from './components/Tiptap.vue'

export default {
  name: 'App',
  components: {
    Tiptap
  }
}
</script>
```

现在你应该可以在浏览器中看到 Tiptap 了。是时候给自己一个鼓励了！:)

## 5. 使用 v-model (可选)
您可能已经习惯了在表单中使用 `v-model` 绑定数据，Tiptap 也支持这种方式。以下是如何在 Tiptap 中使用 `v-model`：

https://embed.tiptap.dev/preview/GuideGettingStarted/VModel