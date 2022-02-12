---
layout: ./scripts/layouts/MainLayout.astro
---

# Codemirror 6

https://codemirror.net/6/

```js
import { EditorState } from "@codemirror/state";
import { EditorView, keymap } from "@codemirror/view";
import { defaultKeymap } from "@codemirror/commands";

let startState = EditorState.create({
  doc: "Hello World",
  extensions: [keymap.of(defaultKeymap)],
});

let view = new EditorView({
  state: startState,
  parent: document.body,
});
```

## 一些概念

### StateField

## 一些操作

### 引入语言包

提供代码高亮、语法提示。

支持语言：https://github.com/codemirror?q=lang

将语言包假如 plugin 中：

```js
import { EditorState, EditorView, basicSetup } from "@codemirror/basic-setup";
import { javascript } from "@codemirror/lang-javascript";

let view = new EditorView({
  state: EditorState.create({ extensions: [basicSetup, javascript()] }),
  parent: document.body,
});
```

### 显示指定代码

创建 state

```js
const state = EditorState.create({
  doc: "some code",
});
```

初始化

```js
let view = new EditorView({
  state,
  parent: document.body,
});
```

更新代码

```js
view.setState(state);
```

### 响应代码变化

使用 StateField.define 创建扩展，并在 state 中使用

```js
const changeExt = StateField.define({
  create() {
    return 0;
  },
  update(v, tr) {
    if (tr.docChanged) {
      onChange(tr.newDoc.toString());
    }
  },
});

EditorState.create({
  extensions: [changeExt],
});
```

### 自动换行

```js
EditorState.create({
  extensions: [EditorView.lineWrapping],
});
```
