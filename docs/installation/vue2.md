# Vue.js 2

## 介绍
以下指南描述了如何将 Tiptap 与您的 [Vue](https://vuejs.org/) CLI 项目集成。

## 要求
* 在您的机器上安装了 [Node](https://nodejs.org/en/download/)
* 在您的机器上安装了 [Vue CLI](https://cli.vuejs.org/)
* 对 [Vue](https://vuejs.org/v2/guide/#Getting-Started) 有经验。

## 1. 创建项目（可选）
如果您已经有一个现有的 Vue 项目，也可以。跳过此步骤并继续下一步。

为了方便起见，让我们从一个名为 `my-tiptap-project` 的全新 Vue 项目开始。Vue CLI 会设置我们需要的一切，只需选择默认的 Vue 2 模板。

```bash
# 创建一个项目
vue create my-tiptap-project

# 切换到项目目录
cd my-tiptap-project
```

## 2. 安装依赖项
好了，够无聊的样板工作了。现在开始安装 Tiptap！以下示例需要使用 `@tiptap/vue-2` 包，`@tiptap/pm`（ProseMirror 库）和包含最常用扩展的 `@tiptap/starter-kit`。

```bash
npm install @tiptap/vue-2 @tiptap/pm @tiptap/starter-kit
```

如果您遵循了步骤 1 和 2，现在可以使用 `npm run dev` 启动您的项目，在您喜欢的浏览器中打开 [http://localhost:8080](http://localhost:8080)。如果您正在使用现有项目，则可能会不同。

## 3. 创建一个新组件
要开始使用 Tiptap，您需要向应用程序添加一个新组件。让我们称之为 `Tiptap` 并将以下示例代码放入 `components/Tiptap.vue` 中。

这是使用 Vue 快速启动 Tiptap 的最快方法。它将为您提供一个非常基本的 Tiptap 版本，没有任何按钮。别担心，您很快就能添加更多功能。

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

## 4. 将其添加到您的应用程序
现在，让我们用以下示例代码替换 `src/App.vue` 的内容，以在应用程序中使用我们的新 `Tiptap` 组件。

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

现在，您应该在浏览器中看到 Tiptap。是时候自我表扬一下啦！ :)

## 5. 使用 v-model（可选）
您可能已经习惯在表单中使用 `v-model` 绑定数据，使用 Tiptap 也可以。这里有一个可用的示例组件，您可以将其集成到您的项目中：

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