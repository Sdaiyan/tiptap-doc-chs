# 文本格式化

https://embed.tiptap.dev/preview/Examples/Formatting

## 描述

Tiptap 能够轻松地帮助我们在编辑器中格式化文本，例如加粗、斜体和下划线等。

## 示例

在上面的链接中，我们提供了一个格式化的示例，你可以在其中输入一些文本并对其进行格式化。 

## 代码

以下代码示例演示了如何使用 Tiptap 中的节点和命令来格式化文本。

```vue
<template>
  <div>
    <tiptap-editor v-model="content" :extensions="extensions" />
  </div>
</template>

<script>
import { Editor } from '@tiptap/core'
import { Bold, Italic, Underline } from '@tiptap/starter-kit'
import { VueNodeViewRenderer } from '@tiptap/vue-2'

export default {
  data() {
    return {
      content: '',
    }
  },
  computed: {
    extensions() {
      return [
        Bold,
        Italic,
        Underline,
        VueNodeViewRenderer({
          Bold: {
            component: {
              template: '<strong><slot /></strong>',
            },
          },
          Italic: {
            component: {
              template: '<em><slot /></em>',
            },
          },
          Underline: {
            component: {
              template: '<u><slot /></u>',
            },
          },
        }),
      ]
    }
  },
  components: {
    TiptapEditor: Editor,
  }
}
</script>
```

## 解释

- 使用 `Bold`、`Italic` 和 `Underline` 命令启用加粗、斜体和下划线。
- 使用 `VueNodeViewRenderer` 渲染器中的自定义 Vue 组件显示加粗、斜体和下划线的节点。