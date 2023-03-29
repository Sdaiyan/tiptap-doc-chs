---
title: Alpine WYSIWYG
tableOfContents: true
---

# Alpine.js

## 介绍
本指南介绍如何将 Tiptap 与 [Alpine.js](https://github.com/alpinejs/alpine) 的第 3 版集成。

在本指南中，我们将使用 [Vite](https://vitejs.dev/) 快速设置一个项目，但你可以使用你习惯的任何工具。Vite 很快，我们喜欢它。

## 要求
* 在你的计算机上安装有 [Node](https://nodejs.org/en/download/)
* 具有 [Alpine.js](https://github.com/alpinejs/alpine) 的使用经验

## 1. 创建项目（可选）
如果你已经有一个现有的 Alpine.js 项目，那也可以。跳过这一步，进行下一步。

假设我们从头开始使用 [Vite](https://vitejs.dev/) 创建一个名为 `my-tiptap-project` 的项目。Vite 可以设置好我们所需的所有东西，只需选择 Vanilla JavaScript 模板即可。

```bash
npm init vite@latest my-tiptap-project -- --template vanilla
cd my-tiptap-project
npm install
npm run dev
```

## 2. 安装依赖项
足以让你脱离枯燥的样板文件。接下来终于可以安装 Tiptap 了！对于下面的示例代码，你需要安装 `alpinejs`、`@tiptap/core` 包、`@tiptap/pm` 包和包含最常用扩展的 `@tiptap/starter-kit`。

```bash
npm install alpinejs @tiptap/core @tiptap/pm @tiptap/starter-kit
```

如果按照第1步的命令行操作，现在可以使用 `npm run dev` 运行项目，并且在喜欢的浏览器中打开 [http://localhost:5173](http://localhost:5173)。如果你正在使用现有项目，这可能会有所不同。

## 3. 初始化编辑器
实际上开始使用 Tiptap，你需要写一点 JavaScript。让我们把以下示例代码放到一个名为 `main.js` 的文件中。

这是使用 Alpine.js 快速启动 Tiptap 的最快方法。这将为你提供 Tiptap 的非常基本的版本。不用担心，你很快就能添加更多功能。

```js
import Alpine from 'alpinejs'
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

document.addEventListener('alpine:init', () => {
  Alpine.data('editor', (content) => {
    let editor

    return {
      updatedAt: Date.now(), // 强制 Alpine 改变选择时更新视图
      init() {
        const _this = this

        editor = new Editor({
          element: this.$refs.element,
          extensions: [
            StarterKit
          ],
          content: content,
          onCreate({ editor }) {
            _this.updatedAt = Date.now()
          },
          onUpdate({ editor }) {
            _this.updatedAt = Date.now()
          },
          onSelectionUpdate({ editor }) {
            _this.updatedAt = Date.now()
          }
        })
      },
      isLoaded() {
        return editor
      },
      isActive(type, opts = {}) {
        return editor.isActive(type, opts)
      },
      toggleHeading(opts) {
        editor.chain().toggleHeading(opts).focus().run()
      },
      toggleBold() {
        editor.chain().toggleBold().focus().run()
      },
      toggleItalic() {
        editor.chain().toggleItalic().focus().run()
      },
    }
  })
})

window.Alpine = Alpine
Alpine.start()
```

## 4. 将其添加到你的应用中
现在，使用以下示例代码替换 `index.html` 的内容，以在我们的应用中使用编辑器。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
</head>
<body>
  <div x-data="editor('<p>Hello world! :-)</p>')">

    <template x-if="isLoaded()">
      <div class="menu">
        <button
          @click="toggleHeading({ level: 1 })"
          :class="{ 'is-active': isActive('heading', { level: 1 }, updatedAt) }"
        >
          H1
        </button>
        <button
          @click="toggleBold()"
          :class="{ 'is-active' : isActive('bold', updatedAt) }"
        >
          Bold
        </button>
        <button
          @click="toggleItalic()"
          :class="{ 'is-active' : isActive('italic', updatedAt) }"
        >
          Italic
        </button>
      </div>
    </template>

    <div x-ref="element"></div>
  </div>

  <script type="module" src="/main.js"></script>

  <style>
    body { margin: 2rem; font-family: sans-serif; }
    button.is-active { background: black; color: white; }
    .ProseMirror { padding: 0.5rem 1rem; margin: 1rem 0; border: 1px solid #ccc; }
  </style>
</body>
</html>
```

现在你应该在浏览器中看到 Tiptap 了。是时候给自己一个鼓励拍一下自己的后背了！ :)