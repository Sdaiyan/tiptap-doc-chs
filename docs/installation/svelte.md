---
title: Svelte 富文本编辑器
tableOfContents: true
---

# Svelte

## 介绍
下面的指南将介绍如何在你的 [SvelteKit](https://kit.svelte.dev/) 项目中集成 Tiptap。

## 快速开始：使用 Svelte REPL 和 Tiptap
如果你只想快速开始，可以使用已安装了 Tiptap 的 [Svelte REPL](https://svelte.dev/repl/798f1b81b9184780aca18d9a005487d2?version=3.31.2)。

## 要求
* 已在你的电脑上安装 [Node.js](https://nodejs.org/en/download/)
* 具备 [Svelte](https://svelte.dev/docs#getting-started) 的使用经验

## 1. 创建一个项目（可选）
如果你已经有了现有的 SvelteKit 项目，那也可以跳过这一步并直接进行下一步。

本指南的示例将从一个名为 `my-tiptap-project` 的全新 SvelteKit 项目开始。下面的命令将设置我们所需的一切。这些命令会询问很多问题，但你只需使用你喜欢的选项或使用默认值。

```bash
npm create svelte@latest my-tiptap-project
cd my-tiptap-project
npm install
npm run dev
```

## 2. 安装依赖项
好了，够无聊的样板代码工作已经做完了。现在，让我们终于安装 Tiptap！对于下面的示例，你需要安装 `@tiptap/core` 包和一些组件，`@tiptap/pm` 和 `@tiptap/starter-kit`，其中包括了最常见的扩展，让你可以快速入门。

```bash
npm install @tiptap/core @tiptap/pm @tiptap/starter-kit
```

如果你已经按照步骤 1 和 2 进行了操作，现在可以使用 `npm run dev` 启动你的项目，并在你喜欢的浏览器中打开 [http://localhost:3000/](http://localhost:3000/)。如果你正在使用现有项目，则可能会有所不同。

## 3. 创建新组件
要真正开始使用 Tiptap，你需要向应用添加一个新组件。我们将其命名为 `Tiptap`，并将以下示例代码放入 `src/lib/Tiptap.svelte` 中。

这是在 SvelteKit 中最快速启动 Tiptap 的方式。它将为你提供一个非常基本的 Tiptap 版本，没有任何按钮。不要担心，你很快就能添加更多功能了。

```html
<script>
  import { onMount, onDestroy } from 'svelte'
  import { Editor } from '@tiptap/core'
  import StarterKit from '@tiptap/starter-kit'

  let element
  let editor

  onMount(() => {
    editor = new Editor({
      element: element,
      extensions: [
        StarterKit,
      ],
      content: '<p>Hello World! 🌍️ </p>',
      onTransaction: () => {
        // 强制重新渲染以使 `editor.isActive` 正常工作
        editor = editor
      },
    })
  })

  onDestroy(() => {
    if (editor) {
      editor.destroy()
    }
  })
</script>

{#if editor}
  <button
    on:click={() => editor.chain().focus().toggleHeading({ level: 1}).run()}
    class:active={editor.isActive('heading', { level: 1 })}
  >
    H1
  </button>
  <button
    on:click={() => editor.chain().focus().toggleHeading({ level: 2 }).run()}
    class:active={editor.isActive('heading', { level: 2 })}
  >
    H2
  </button>
  <button on:click={() => editor.chain().focus().setParagraph().run()} class:active={editor.isActive('paragraph')}>
    P
  </button>
{/if}

<div bind:this={element} />

<style>
  button.active {
    background: black;
    color: white;
  }
</style>
```

## 4. 将组件添加到你的应用中
现在，让我们将 `src/routes/+page.svelte` 的内容替换为以下示例代码，以在我们的应用中使用新的 `Tiptap` 组件。

```html
<script>
  import Tiptap from '$lib/Tiptap.svelte'
</script>

<main>
  <Tiptap />
</main>
```

现在你应该可以在浏览器中看到 Tiptap 了，赶快给自己一个大大的夸奖吧！ :)