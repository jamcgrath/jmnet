---
title: Running JS from a string without eval
date: "2020-01-27"
thumb_img_path: /images/drake.jpg
content_img_path:
alt_text:
template: post
excerpt: >-
  Let's look at how to execute javascript from a string without using eval.
---

Maybe you have heard that "`eval` is evil?" If you haven't take a few minutes to read <a href="https://humanwhocodes.com/blog/2013/06/25/eval-isnt-evil-just-misunderstood/">eval() isn’t evil, just misunderstood</a>.

Without going deep into it, reasons for not using `eval` are:

- Security
- Performance
- Debugging can be tricky
- General misuse

As an alternative to `eval`, the `Function` constructor can be used to run Js from a string. The following codepen uses it to add a click event to the button.

<p class="codepen" data-height="376" data-theme-id="32872" data-default-tab="result" data-user="jamcgrath" data-slug-hash="GRgepeR" style="height: 376px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Execute JS in String">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/GRgepeR">
  Execute JS in String</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

What is happening is that the constructor is dynamically creating a function that runs only in the global scope. However it still suffers from some issues that `eval` has such as security and performance, but faster. This can be confirmed by doing this <a href="https://www.measurethat.net/Benchmarks/Show/2858/0/eval-vs-new-function">`new Function()` vs `eval()` test</a> Also because the code is a string it may prevent some JS engine optimizations.

```js
new Function([arg1, arg2, ...argN], functionBody);
```

The code block above is the syntax of the `Function` constructor. It takes strings as it's parameters. The `arg` parameters are passed to the `functionBody`. The arguments for the `functionBody` can be writtern as `'arg1', 'arg2'` or `'arg1, arg2'` or as `'arg1 , arg2'`.

The next codeblock logs to the console the multiplication of two numbers.

```js
const f = new Function("a", "b", "return console.log(a * b)");
f(10, 10); //100
```

For more information check out these links:

<a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function">
Function constructor at MDN</a>

<a href="https://javascript.info/new-function">The "new Function" syntax at javascript.info</a>
