# 使用 TypeScript

## 简介

整个 Tiptap 代码库都是用 TypeScript 编写的。如果你没有听说过或者从未使用过它，没关系，你也不需要使用。

TypeScript 通过添加类型（因此得名）扩展了 JavaScript。它添加了新的语法，这些语法在原始的 JavaScript 中并不存在。实际上，这些语法在运行在浏览器之前会被移除，但这一步——编译——对于尽早发现错误非常重要。它检查你是否向函数传递了正确类型的数据。对于一个庞大而复杂的项目，这非常有价值。这意味着我们将在将代码交付给你之前收到许多错误通知。

**无论如何，如果你的项目中没有使用 TypeScript，也没有关系。** 你仍然可以使用 Tiptap，并获得 Tiptap API 的良好自动完成（如果你的编辑器支持的话，但大多数编辑器都支持）。

如果你在项目中使用 TypeScript 并想要扩展 Tiptap，有两种类型是很好了解的。

## [#](https://tiptap.dev/guide/typescript#types)类型

### [#](https://tiptap.dev/guide/typescript#options-types)选项类型

为了扩展或创建默认选项，你需要定义一个自定义类型，以下是一个示例：

```typescript
import { Extension } from '@tiptap/core'

export interface CustomExtensionOptions {
  awesomeness: number,
}

const CustomExtension = Extension.create<CustomExtensionOptions>({
  addOptions() {
    return {
      awesomeness: 100,
    }
  },
})
```

### [#](https://tiptap.dev/guide/typescript#storage-types)存储类型

为了为扩展的存储添加类型，你需要将其作为第二个类型参数传递。

```typescript
import { Extension } from '@tiptap/core'

export interface CustomExtensionStorage {
  awesomeness: number,
}

const CustomExtension = Extension.create<{}, CustomExtensionStorage>({
  name: 'customExtension',

  addStorage() {
    return {
      awesomeness: 100,
    }
  },
})
```

当在扩展之外使用存储时，你必须手动设置类型。

```javascript
import { CustomExtensionStorage } from './custom-extension'

const customStorage = editor.storage.customExtension as CustomExtensionStorage
```

### [#](https://tiptap.dev/guide/typescript#command-type)Command 类型

核心包还导出了一个 `Command` 类型，需要将其添加到您在代码中指定的所有命令中。以下是一个示例：

```typescript
import { Extension } from '@tiptap/core'

declare module '@tiptap/core' {
  interface Commands<ReturnType> {
    customExtension: {
      /**
       * Comments will be added to the autocomplete.
       */
      yourCommand: (someProp: any) => ReturnType,
    }
  }
}

const CustomExtension = Extension.create({
  addCommands() {
    return {
      yourCommand: someProp => ({ commands }) => {
        // …
      },
    }
  },
})
```

基本上就是这样。我们将自动处理其余的部分。