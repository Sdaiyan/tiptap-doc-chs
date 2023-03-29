# Tiptap

> 一个强大的基于 Vue.js 的富文本编辑器

Tiptap 是基于 Vue.js 和 ProseMirror 的富文本编辑器，它可以帮助你创建一流的编辑体验。它具有模块化的体系结构并且易于扩展和自定义。它是一个完全可组合的编辑器，这意味着你可以使用自己的 ProseMirror 插件来扩展它。

## 特性

* 非常易于扩展和自定义
* 具有模块化的体系结构
* 全局键盘快捷键
* 无缝整合任意验证器
* 即时预览
* TODO：补充更多细节介绍

## 安装

```bash
npm install tiptap
```

## 基本用法

```vue
<template>
  <div>
    <editor :content="content" @update="updateContent" />
  </div>
</template>

<script>
import { Editor } from 'tiptap'
import StarterKit from 'tiptap-extensions/dist/starter-kit'

export default {
  components: {
    Editor,
  },
  data() {
    return {
      content: '<p>Hello World! 🌎️</p>',
    }
  },
  methods: {
    updateContent({ content, text }) {
      this.content = content
    },
  },
  created() {
    this.editor = new Editor({
      content: this.content,
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

更多信息请参考[官方文档](https://www.tiptap.dev/)。