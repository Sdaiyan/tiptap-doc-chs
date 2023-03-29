# CDN
:::warning
目前 [skypack 存在一些问题](https://github.com/skypackjs/skypack-cdn/issues/159) ，可能会时不时遇到问题。我们暂时无法解决这个问题。
:::

如果是测试或演示，可以使用我们的 [Skypack](https://www.skypack.dev/) CDN 构建。以下是开始所需的几行代码：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <div class="element"></div>
  <script type="module">
    import { Editor } from 'https://cdn.skypack.dev/@tiptap/core?min'
    import StarterKit from 'https://cdn.skypack.dev/@tiptap/starter-kit?min'
    const editor = new Editor({
      element: document.querySelector('.element'),
      extensions: [
        StarterKit,
      ],
      content: '<p>Hello World!</p>',
    })
  </script>
</body>
</html>
```

现在您应该在浏览器中看到 Tiptap。现在自己给自己点个赞吧！ :)