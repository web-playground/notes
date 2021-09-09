# 预览方案

把代码中的运行结果显示在页面上

## Dom

直接在同一文档下的节点中预览内容，如 div 元素。可用于 CSS demo 预览，同一 CSS 属性多个值比较。

需要修改 CSS rule 的每个选择器，在前面拼接上包裹容器。需要构造 CSSStyleSheet 实例， Firefox 对此目前还是个实验性功能，需要手动开启此功能 (about:config 中打开 layout.css.constructable-stylesheets.enabled).

## Shadow DOM

Shadow DOM 可以隔离内外的 CSS，是 CSS 效果预览的不错方案。

在预览 HTML 时，由于还在同一文档中，对 id 的指向总会指向页面上的第一个，即使这些相同的 id 是在不同的 Shadow Root 下。

## iframe

可以隔离 document，可以直接将拼接的代码效果预览出来。

设置代码方式：

- `iframe.contentDocument.body.innerHTML = htmlCode` 可以预览 HTML、CSS，JS 代码不执行
- `iframe.setAttribute('srcdoc', htmlCode)` 可正常执行 JS 代码，可以进行涉及 DOM 的预览

## Web Worker + Console

可以在 worker 线程中直接运行代码，对于没有界面（DOM）的 JS core 预览比较方便，可以在 DevTools 中看到运行结果。
