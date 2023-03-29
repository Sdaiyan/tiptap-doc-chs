# 气泡菜单

[![Version](https://img.shields.io/npm/v/@tiptap/extension-bubble-menu.svg?label=version)](https://www.npmjs.com/package/@tiptap/extension-bubble-menu)
[![Downloads](https://img.shields.io/npm/dm/@tiptap/extension-bubble-menu.svg)](https://npmcharts.com/compare/@tiptap/extension-bubble-menu?minimal=true)

这个扩展能让一个上下文菜单在选中文本旁边出现。用它来让用户为文本选择应用[格式](/api/marks)。

同样，标记和样式完全由你控制。

## 安装
```bash
npm install @tiptap/extension-bubble-menu
```

## 配置

### element
包含菜单的 DOM 元素。

类型：`HTMLElement`

默认值： `null`

### updateDelay
`BubbleMenu`使用了防抖的方法来防止菜单在每次选择更新时更新。可以通过毫秒数来控制。`BubbleMenuPlugin`将默认延迟 250ms。设置 delay 参数为 `0` 可以取消防抖处理。

类型：`Number`

默认值：`undefined`

### tippyOptions
在底层，`BubbleMenu`使用了 [tippy.js](https://atomiks.github.io/tippyjs/v6/all-props/)。您可以直接传递选项。

类型：`Object`

默认值：`{}`

### pluginKey
用于底层 ProseMirror 插件的键。如果添加多个实例，请确保使用不同的键值。

类型：`string | PluginKey`

默认值：`'bubbleMenu'`

### shouldShow
控制菜单是否应该显示的回调。

类型：`(props) => boolean`

## 源代码
[packages/extension-bubble-menu/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-bubble-menu/)

## 用法

### JavaScript
```js
import { Editor } from '@tiptap/core'
import BubbleMenu from '@tiptap/extension-bubble-menu'

new Editor({
  extensions: [
    BubbleMenu.configure({
      element: document.querySelector('.menu'),
    }),
  ],
})
```

### 框架
https://embed.tiptap.dev/preview/Extensions/BubbleMenu

### 自定义逻辑
通过 `shouldShow` 选项自定义显示菜单的逻辑。对于组件，可以将 `shouldShow` 作为属性传递。

```js
BubbleMenu.configure({
  shouldShow: ({ editor, view, state, oldState, from, to }) => {
    // 只为图片和链接显示气泡菜单
    return editor.isActive('image') || editor.isActive('link')
  },
})
```

### 多个菜单
通过设置唯一的 `pluginKey` 来使用多个菜单。

```js
import { Editor } from '@tiptap/core'
import BubbleMenu from '@tiptap/extension-bubble-menu'

new Editor({
  extensions: [
    BubbleMenu.configure({
      pluginKey: 'bubbleMenuOne',
      element: document.querySelector('.menu-one'),
    }),
    BubbleMenu.configure({
      pluginKey: 'bubbleMenuTwo',
      element: document.querySelector('.menu-two'),
    }),
  ],
})
```

您也可以传递一个 ProseMirror 的 `PluginKey`。

```js
import { Editor } from '@tiptap/core'
import BubbleMenu from '@tiptap/extension-bubble-menu'
import { PluginKey } from '@tiptap/pm/state'

new Editor({
  extensions: [
    BubbleMenu.configure({
      pluginKey: new PluginKey("bubbleMenuOne"),
      element: document.querySelector('.menu-one'),
    }),
    BubbleMenu.configure({
      pluginKey: new PluginKey("bubbleMenuTwo"),
      element: document.querySelector('.menu-two'),
    }),
  ],
})
```