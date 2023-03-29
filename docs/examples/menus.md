# 菜单

https://embed.tiptap.dev/preview/Examples/Menus

在 tiptap 中，菜单由多个按钮和下拉菜单组成。这些按钮和下拉菜单用于插入或编辑文本内容。

要使用菜单，您需要在编辑器中安装菜单插件。接下来，您可以使用菜单 API 将按钮或下拉菜单添加到菜单中。

以下是一个菜单的例子：

```javascript
import { MenuBar } from 'tiptap-extensions'

const menu = new MenuBar({
  editor,
  floating: true,
  menuClass: 'menu',
  dropdownClass: 'dropdown',
  commands: {
    // insert or toggle mark here
  },
  content: [
    // menu items here
  ],
  onUpdate({ state }) {
    // change button states here
  },
})
```

在此示例中，我们使用 `MenuBar` 插件创建了一个菜单。我们还向它传入了一些选项。

- `editor` 是我们将要使用的编辑器。

- `floating` 选项指定菜单是否应浮动。默认情况下，该选项为 `false`，菜单将显示在编辑器的顶部。如果设置为 `true`，则菜单将浮动并可以调整其位置。

- `menuClass` 和 `dropdownClass` 选项指定菜单和下拉菜单的 CSS 类。

- `commands` 选项传入命令方法对象。命令方法定义了我们将要执行的具体操作，例如插入或切换标记。

- `content` 选项定义了在菜单中显示的菜单项。菜单项可以是分隔符、按钮或下拉菜单。 默认情况下，菜单将在编辑器的左侧坐标处显示。

- `onUpdate` 选项用于在菜单状态更新时执行自定义代码。在这个回调中，您将能够更改按钮的状态。

有关更多信息，请查看相关文档。