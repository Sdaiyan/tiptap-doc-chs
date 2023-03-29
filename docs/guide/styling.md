# 样式

## 简介

Tiptap 是无样式的，这意味着没有提供样式。这也意味着，您完全控制编辑器的外观。以下方法允许您向编辑器应用自定义样式。

## [#](https://tiptap.dev/guide/styling#option-1-style-the-plain-html)选项1：为纯HTML样式

整个编辑器都在具有类`.ProseMirror`的容器内呈现。您可以使用它来将样式限定于编辑器内容：

```css
/* 限定于编辑器 */
.ProseMirror p {
  margin: 1em 0;
}
```

如果您在其他位置呈现存储的内容，就不会有`.ProseMirror`容器，因此您可以全局添加用到的HTML标签的样式：

```css
/* 全局样式 */
p {
  margin: 1em 0;
}
```

## [#](https://tiptap.dev/guide/styling#option-2-add-custom-classes)选项2：添加自定义类

您可以控制整个呈现，包括为所有内容添加类。

### [#](https://tiptap.dev/guide/styling#extensions)扩展

大多数扩展允许您通过`HTMLAttributes`选项向呈现的HTML添加属性。您可以使用它来添加自定义类（或任何其他属性）。当您使用[Tailwind CSS](https://tailwindcss.com/)时，这也非常有帮助。

```javascript
new Editor({
  extensions: [
    Document,
    Paragraph.configure({
      HTMLAttributes: {
        class: 'my-custom-paragraph',
      },
    }),
    Heading.configure({
      HTMLAttributes: {
        class: 'my-custom-heading',
      },
    }),
    Text,
  ],
})
```

呈现的HTML将如下所示：

```html
<h1 class="my-custom-heading">Example Text</p>
<p class="my-custom-paragraph">Wow, that’s really custom.</p>
```

如果扩展已经定义了类，则会添加您的类。

### [#](https://tiptap.dev/guide/styling#editor)编辑器

您甚至可以像这样将类传递给包含编辑器的元素：

```javascript
new Editor({
  editorProps: {
    attributes: {
      class: 'prose prose-sm sm:prose lg:prose-lg xl:prose-2xl mx-auto focus:outline-none',
    },
  },
})
```

### [#](https://tiptap.dev/guide/styling#with-tailwind-css)使用Tailwind CSS

编辑器也可以与Tailwind CSS一起使用。以下是使用`@tailwindcss/typography`插件进行样式处理的示例。

<iframe src="https://embed.tiptap.dev/preview/Experiments/Tailwind?inline=false&amp;hideSource=false" width="100%" height="0" frameborder="0"></iframe>

## [#](https://tiptap.dev/guide/styling#option-3-customize-the-html)选项三：自定义 HTML

你也可以自定义扩展的标记。以下示例将创建一个自定义粗体扩展，它不会呈现 `<strong>` 标记，而是 `<b>` 标记：

```javascript
import Bold from '@tiptap/extension-bold'

const CustomBold = Bold.extend({
  renderHTML({ HTMLAttributes }) {
    // 原本：
    // return ['strong', HTMLAttributes, 0]
    return ['b', HTMLAttributes, 0]
  },
})

new Editor({
  extensions: [
    // …
    CustomBold,
  ],
})
```

你应该将自定义扩展放在单独的文件中，但我想你已经明白了。