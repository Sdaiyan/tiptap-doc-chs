---
title: Nuxt.js WYSIWYG
tableOfContents: true
---

# Nuxt.js

## 简介
本指南介绍如何将 Tiptap 与您的 [Nuxt.js](https://nuxtjs.org/) 项目集成。

## 要求
* 在您的计算机上安装 [Node](https://nodejs.org/en/download/)
* 了解 [Vue](https://vuejs.org/v2/guide/#Getting-Started)

## 1. 创建项目 (可选)
如果您已经有一个现有的 Vue 项目，也可以。跳过此步骤，进入下一步。

为了本指南，让我们从一个名为`my-tiptap-project`的新的 Nuxt.js 项目开始。以下命令设置我们需要的一切。它会问很多问题，但只需使用你想要的或使用默认设置即可。

```bash
# 创建项目
npm init nuxt-app my-tiptap-project

# 切换目录
cd my-tiptap-project
```

## 2. 安装依赖
好了，已经处理完了无聊的样板文件。现在，让我们终于安装 Tiptap！对于以下示例，您需要 `@tiptap/vue-2` 包及其几个组件，`@tiptap/pm` 包和 `@tiptap/starter-kit`，它具有最常见的扩展，可快速入门。

```bash
npm install @tiptap/vue-2 @tiptap/pm @tiptap/starter-kit
```

如果您按照步骤 1 和 2，现在就可以使用`npm run serve`启动项目，并在您喜欢的浏览器中打开[http://localhost:8080/](http://localhost:8080/)。如果您在使用现有项目，则可能会有所不同。

## 3. 创建新组件
为了开始使用 Tiptap，您需要向应用程序中添加一个新组件。我们将其称为`TiptapEditor`，并将以下示例代码放在`components / TiptapEditor.vue`中。

这是在 Vue 中开始使用 Tiptap 的最快方法。它会为您提供一个非常基本的 Tiptap 版本，没有任何按钮。别担心，您很快就可以添加更多功能。

```html
<template>
  <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-2'
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

  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>
```

## 4. 将其添加到您的应用程序中
现在，让我们将 `pages / index.vue` 的内容替换为以下示例代码，以在我们的应用程序中使用新的 `TiptapEditor` 组件。

```html
<template>
  <div>
    <client-only>
      <tiptap-editor />
    </client-only>
  </div>
</template>

<script>
import TiptapEditor from '~/components/TiptapEditor.vue'
export default {
  components: {
    TiptapEditor
  }
}
</script>
```

请注意，Tiptap 需要在客户端而不是服务器上运行。需要在`<client-only>`标签中包装编辑器。[了解有关仅客户端组件的更多信息。](https://nuxtjs.org/api/components-client-only)

现在，您应该在浏览器中看到 Tiptap。该自我表扬了！ :)

## 5. 使用 v-model (可选)
您可能已经习惯了在表单中使用`v-model`绑定您的数据，Tiptap 也支持此操作。以下是可以集成到项目中的工作示例组件：

https://embed.tiptap.dev/preview/GuideGettingStarted/VModel

```html
<template>
  <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-2'
import StarterKit from '@tiptap/starter-kit'

export default {
  components: {
    EditorContent,
  },

  props: {
    value: {
      type: String,
      default: '',
    },
  },

  data() {
    return {
      editor: null,
    }
  },

  watch: {
    value(value) {
      // HTML
      const isSame = this.editor.getHTML() === value

      // JSON
      // const isSame = JSON.stringify(this.editor.getJSON()) === JSON.stringify(value)

      if (isSame) {
        return
      }

      this.editor.commands.setContent(value, false)
    },
  },

  mounted() {
    this.editor = new Editor({
      content: this.value,
      extensions: [
        StarterKit,
      ],
      onUpdate: () => {
        // HTML
        this.$emit('input', this.editor.getHTML())

        // JSON
        // this.$emit('input', this.editor.getJSON())
      },
    })
  },

  beforeDestroy() {
    this.editor.destroy()
  },
}
</script>
```