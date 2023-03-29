---
title: PHP WYSIWYG
tableOfContents: true
---
# PHP

## 介绍
你可以在 Laravel、Livewire、Inertia.js、[Alpine.js](/installation/alpine)、[Tailwind CSS](/guide/styling#with-tailwind-css)上使用 Tiptap，甚至在 PHP 中使用。

## Tiptap for PHP
我们提供了[一个官方的 PHP 包，用于处理 Tiptap 内容](/api/utilities/tiptap-php)。一个处理 Tiptap 内容的 PHP 包。你可以将 Tiptap 兼容的 JSON 转换为 HTML，或反过来，可以对它进行清理或修改等操作。

## Laravel Livewire

### my-livewire-component.blade.php
```html
<!--
  在你的 Livewire 组件中，你可以添加一个
  autosave 方法来处理每 10 秒保存编辑器中的内容
-->
<x-editor
  wire:model="foo"
  wire:poll.10000ms="autosave"
></x-editor>
```

### editor.blade.php
```html
<div
  x-data="setupEditor(
    $wire.entangle('{{ $attributes->wire('model')->value() }}').defer
  )"
  x-init="() => init($refs.editor)"
  wire:ignore
  {{ $attributes->whereDoesntStartWith('wire:model') }}
>
  <div x-ref="editor"></div>
</div>
```

### index.js
```js
import { Editor } from '@tiptap/core'
import StarterKit from '@tiptap/starter-kit'

window.setupEditor = function (content) {
  let editor

  return {
    content: content,

    init(element) {
      editor = new Editor({
        element: element,
        extensions: [
          StarterKit,
        ],
        content: this.content,
        onUpdate: ({ editor }) => {
          this.content = editor.getHTML()
        }
      })

      this.$watch('content', (content) => {
        // 如果新内容与 TipTap 的相同，则跳过。
        if (content === editor.getHTML()) return

        /*
          否则，这意味着一个力量外部于 TipTap
          修改了这个 Alpine 组件上的数据，
          这可能是 Livewire 自己。
          在这种情况下，我们只需要更新 TipTap 的内容即可。
          关于 `setContent()` 方法的更多信息，请参见：
            https://www.tiptap.dev/api/commands/set-content
        */
        editor.commands.setContent(content, false)
      })
    }
  }
}
```