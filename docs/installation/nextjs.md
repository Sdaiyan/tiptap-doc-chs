---
title：Next.js 富文本编辑器
tableOfContents: true
---

# Next.js

## 简介
本指南介绍如何将 Tiptap 集成到[Next.js](https://nextjs.org/) 项目中。

## 需求
* 在机器上安装了 [Node](https://nodejs.org/en/download/)
* 熟悉 [React](https://reactjs.org/) 技术

## 1. 创建项目（可选）
如果您已有现有的 Next.js 项目，那也没关系。跳过此步骤，继续下一步。

为了本指南的目的，让我们从创建一个名为 `my-tiptap-project` 的新 Next.js 项目。以下命令设置了开始所需的所有内容。 
```bash
# 创建一个项目
npx create-next-app my-tiptap-project

# 更改目录
cd my-tiptap-project
```

## 2. 安装依赖项
现在，我们已经设置好了标准的样板，可以开始使用 Tiptap 了！为此，我们需要安装三个包：`@tiptap/react`，`@tiptap/pm` 和包含快速入门所需的所有扩展的 `@tiptap/starter-kit`。

```bash
npm install @tiptap/react @tiptap/pm @tiptap/starter-kit
```

如果您遵循了第 1 和第 2 步，现在可以使用 `npm run dev` 启动您的项目，并在喜爱的浏览器中打开 [http://localhost:3000/](http://localhost:3000/)。如果您正在使用现有项目，则可能会有所不同。

## 3. 创建新组件
要实际开始使用 Tiptap，您需要向应用程序添加一个新的组件。要执行此操作，首先创建一个名为 `components/` 的目录。现在，需要创建我们的组件，我们称为 `Tiptap`。将以下示例代码放在 `/components/Tiptap.js` 中，它有助于完成此操作。

```jsx
import { useEditor, EditorContent } from '@tiptap/react'
import StarterKit from '@tiptap/starter-kit'

const Tiptap = () => {
  const editor = useEditor({
    extensions: [
      StarterKit,
    ],
    content: '<p>Hello World! 🌎️</p>',
  })

  return (
    <EditorContent editor={editor} />
  )
}

export default Tiptap
```

## 4. 将其添加到您的应用程序中
现在，用以下示例代码替换 `pages/index.js` 的内容，以在应用程序中使用我们的新 `Tiptap` 组件。

```jsx
import Tiptap from '../components/Tiptap'

export default function Home() {
    return (
         <Tiptap />
    )
}
```
现在您应该在浏览器中看到 Tiptap。时间给自己一个好评! :)