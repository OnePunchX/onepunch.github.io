---
title: React 合成事件
date: 2020-06-17 15:44:29
tags: react合成事件
categories: 前端
---

这个不是很重要，而且想真弄懂，得看源码。我看的是一头雾水。但是大概思路可以表达出来

### React 合成事件一套机制：React 并不是将 click 事件直接绑定在 dom 上面，而是采用事件冒泡的形式冒泡到 document 上面，当事件发生并冒泡至 document 处时，React 将事件内容封装交给中间层 SyntheticEvent（负责所有事件合成），然后 React 将事件封装给正式的函数处理运行和处理。

为啥有这种 react 合成事件 这种东西？ 存在即合理。
如果 dom 上绑定了特别多的事件处理函数，那指定会卡。为了不会卡，所以有了这个 react 合成事件，并且对浏览器兼容性，不用担心 ie 的坑了。

### 注意：React 事件和原生事件最好不要混用。原生事件中如果执行了 stopPropagation 方法，则会导致其他 React 事件失效。因为所有元素的事件将无法冒泡到 document 上，导致所有的 React 事件都将无法被触发。

下面留个链接，是大佬分析源码的东西。
[点击跳转](https://zhuanlan.zhihu.com/p/25883536)