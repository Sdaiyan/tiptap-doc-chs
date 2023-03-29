# React

## 介绍
以下指南描述了如何将 Tiptap 与您的 [React](https://reactjs.org/) 项目集成。我们这里使用了 [Create React App](https://reactjs.org/docs/getting-started.html)，但是使用其他设置的工作流程应该也是类似的。

## 创建 React 应用程序

### 快速开始
如果您只想快速开始使用 Tiptap，可以使用 [Tiptap Create React App 模板 @alb](https://github.com/alb/cra-template-tiptap) 来创建一个新项目，其中所有下面列出的步骤都已经完成。

```bash
npx create-react-app my-tiptap-project --template tiptap
```

### 逐步操作
下面列出了所有步骤，但是如果您更喜欢观看视频教程，我们也有一些视频供您参考：

https://tiptap.dev/screencasts/installation/install-tiptap-with-create-react-app

#### 1. 创建项目 (可选)
首先，我们创建一个名为 `my-tiptap-project` 的全新的 React 项目。[Create React App](https://reactjs.org/docs/getting-started.html) 将为我们设置好一切。

```bash
# 用 npm 创建项目
npx create-react-app my-tiptap-project

# 切换到项目目录
cd my-tiptap-project
```

#### 2. 安装依赖项
现在是时候安装 `@tiptap/react` 包、`@tiptap/pm` (ProseMirror 库) 和 `@tiptap/starter-kit` 扩展库了。 `@tiptap/starter-kit` 包含了最常用的扩展，可以帮助您快速入手。

```bash
npm install @tiptap/react @tiptap/pm @tiptap/starter-kit
```

如果您按照步骤 1 和 2 进行操作，现在可以使用 `npm run start` 启动项目，并在浏览器中打开 [http://localhost:3000](http://localhost:3000)。

#### 3. 创建新组件
为了实际开始使用 Tiptap，我们需要创建一个新组件。让我们把它命名为 `Tiptap`，并将以下示例代码放入 `src/Tiptap.jsx` 中。

```jsx
// src/Tiptap.jsx
import { useEditor, EditorContent } from '@tiptap/react'
import StarterKit from '@tiptap/starter-kit'

const Tiptap = () => {
  const editor = useEditor({
    extensions: [
      StarterKit,
    ],
    content: '<p>Hello World!</p>',
  })

  return (
    <EditorContent editor={editor} />
  )
}

export default Tiptap
```

#### 4. 将其添加到应用程序中
最后，将 `src/App.js` 的内容替换为我们的新 `Tiptap` 组件。

```jsx
import Tiptap from './Tiptap.jsx'

const App = () => {
  return (
    <div className="App">
      <Tiptap />
    </div>
  )
}

export default App
```

现在您应该可以在浏览器中看到一个相当基础的 Tiptap 示例了。

#### 5. 完整设置 (可选)
准备好它更酷炫的功能吗？下面的演示展示了如何设置基本工具栏。随意借鉴并根据您的需要进行自定义：

https://embed.tiptap.dev/preview/Examples/Default