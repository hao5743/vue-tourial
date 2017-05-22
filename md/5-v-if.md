## 条件渲染

使用`v-if`条件渲染

```html
<h1 v-if="ok">Yes</h1>
<h1 v-else>No</h1>
```

### template条件组

有时我们需要切换多个元素，可以使用`<template>`元素当做包装元素，最终渲染结果不包括`template`元素

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

### else和else-if

```html
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>
```
类似于 v-else，,v-else-if 必须紧跟在 v-if 或者 v-else-if 元素之后。

### 用key管理可重复元素

ue 会尽可能高效地渲染元素，通常会复用已有元素而不是从头开始渲染。

比如：

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>
```

那么在上面的代码中切换 loginType 将不会清除用户已经输入的内容。因为两个模版使用了相同的元素，`<input>` 不会被替换掉——仅仅是替换了它的的 placeholder。

如果我们需要两个不同的`<input>`元素怎么办呢？答案是，使用`<key>`属性，例子：

```html
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```
现在，每次切换时，输入框都将被重新渲染。注意, `<label>` 元素仍然会被高效地复用，因为它们没有添加 key 属性。

### v-show和v-if比较

另一个用于根据条件展示元素的选项是 v-show 指令:
```html
<h1 v-show="ok">Hello!</h1>
```
> 注意: `v-show` 的元素始终会被渲染并保留在 DOM 中，她只是简单地切换元素的 CSS 属性 `display` 。

> 注意: v-show 不支持 `<template>` 语法，也不支持 `v-else`。

不同点：

`v-if` 是“真正的”条件渲染，因为它会确保在切换过程中条件块内的事件监听器和 子组件适当地被销毁和重建。

`v-if` 也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。而 `v-show` 不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，`v-if` 有**更高的切换开销**，而 `v-show` 有**更高的初始渲染开销**。因此，如果需要非常频繁地切换，则使用 v-show 较好；如果在运行时条件不太可能改变，则使用 v-if 较好。