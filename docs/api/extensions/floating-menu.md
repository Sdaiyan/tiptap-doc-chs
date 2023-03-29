# 浮动菜单

此扩展将在空行出现菜单。

## 安装

```bash
npm install @tiptap/extension-floating-menu
```

## 设置

### element

包含菜单的 DOM 元素。

类型：`HTMLElement`

默认值：`null`

### tippyOptions

在幕后，`FloatingMenu` 使用[tippy.js](https://atomiks.github.io/tippyjs/v6/all-props/)。您可以直接传递选项。

类型：`Object`

默认值：`{}`

### pluginKey

潜在的 ProseMirror 插件的键。如果添加多个实例，请确保使用不同的键。

类型：`string | PluginKey`

默认值：`'floatingMenu'`

### shouldShow

用于控制是否应显示菜单的回调。

类型：`(props) => boolean`

## 源代码

[packages/extension-floating-menu/](https://github.com/ueberdosis/tiptap/blob/main/packages/extension-floating-menu/)

## 使用原生 JavaScript

```js
import { Editor } from '@tiptap/core'
import FloatingMenu from '@tiptap/extension-floating-menu'

new Editor({
  extensions: [
    FloatingMenu.configure({
      element: document.querySelector('.menu'),
    }),
  ],
})
```

## 使用框架

https://embed.tiptap.dev/preview/Extensions/FloatingMenu

### 自定义逻辑

使用 `shouldShow` 选项自定义菜单显示逻辑。对于组件，可以将 `shouldShow` 作为 prop 传递。

```js
FloatingMenu.configure({
  shouldShow: ({ editor, view, state, oldState }) => {
    // 在任何段落中展示菜单
    return editor.isActive('paragraph')
  },
})
```

### 多个菜单

通过设置唯一的 `pluginKey` 使用多个菜单。

```js
import { Editor } from '@tiptap/core'
import FloatingMenu from '@tiptap/extension-floating-menu'

new Editor({
  extensions: [
    FloatingMenu.configure({
      pluginKey: 'floatingMenuOne',
      element: document.querySelector('.menu-one'),
    }),
    FloatingMenu.configure({
      pluginKey: 'floatingMenuTwo',
      element: document.querySelector('.menu-two'),
    }),
  ],
})
```

或者，您可以传递 ProseMirror `PluginKey`。

```js
import { Editor } from '@tiptap/core'
import FloatingMenu from '@tiptap/extension-floating-menu'
import { PluginKey } from '@tiptap/pm/state'

new Editor({
  extensions: [
    FloatingMenu.configure({
      pluginKey: new PluginKey('floatingMenuOne'),
      element: document.querySelector('.menu-one'),
    }),
    FloatingMenu.configure({
      pluginKey: new PluginKey('floatingMenuOne'),
      element: document.querySelector('.menu-two'),
    }),
  ],
})
```