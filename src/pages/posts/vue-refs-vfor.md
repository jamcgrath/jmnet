---
title: Using refs in a v-for loop
date: "2020-02-23"
thumb_img_path: images/v-for-refs.png
content_img_path:
alt_text:
template: post
excerpt: You can do a couple of interesting things in a v-for with refs in vue
---

Refs are a really cool feature in Vue. You can do some neat things when used in a `v-for` loop.

The <a href="https://vuejs.org/v2/api/#ref">Vue documentation for refs</a> says that if you use it on a dom elememt it will reference just that dom element. If used on a component it references the component instance. If it's used in a `v-for` loop, Vue creates an array of elements or components.

Here's a codepen I made illustrating a few ways to use refs in a `v-for` loop.

<p class="codepen" data-height="429" data-theme-id="32872" data-default-tab="result" data-user="jamcgrath" data-slug-hash="vYOLpdY" style="height: 429px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Refs in v-for">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/vYOLpdY">
  Refs in v-for</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

All of the examples references arrays. In the first example the same `ref` is applied to all the `li` in the list. This results in Vue creating a single array.

```
  <li v-for="(obj, index) in dataObj" :key="`vfor-${index}`" ref="listItem" class="v-for-li">{{obj.item}}</li>
```

Vue tools show that it's a array named "listItem" with 7 elements.

<img src="/images/v-for-ref-single-array.png" />

In the second example the `ref` is assigned using a ternary. This results in Vue creating 2 arrays. The data object that is being looped over has an item with a boolean value which is used for the ternary.

```
 <li v-for="(obj, index) in dataObj" :key="`ternary${index}`" :ref="obj.even ? 'expr-1' : 'expr-2'">{{obj.item}}</li>
```

Vue tools show 2 arrays named "expr-1" and "expr-2".

<img src="/images/v-for-ref-ternary.png" />

The last example in the codepen has a the `ref` being assigned with a function. This creates multiple arrays. If the index of the loop modulo 2 equals zero, the element is assigned to an array named "func-item-mod-2". Otherwise the element is assigned to an array named "func-item" with the index appended to it. If ES6 interpolation is not used the function will not be called.

```
<li v-for="(obj, index) in dataObj" :key="`function${index}`" :ref="`${funcRef(index)}`" class="func-item"
      :class="`func-${index}`">

//function method
  funcRef(index) {
    return (index % 2 === 0 ) ? 'funcItem-mod-2' :`funcItem-${index}`;
  }
```

Vue tools shows 4 arrays.

<img src="/images/v-for-ref-function.png" />

There are a couple of caveats to usig `refs` in a `v-for`.

1. If it's being assigned a dynamic name it needs to be binded. `v-bind:ref` or `:ref`.
2. When creating multiple arrays, an element can only be assigned to one array. Each array will be unique.
3. When using a function it needs to be interpolated `` :ref="\`${()=>'refName'}\`" ``.
4. Refs can't be assigned with multiple functions. Although an array of functions can be used but the results will not meet expectations.

```
:ref="[func1(), func2()]"

// func1[]
// ,[]
//func2[]

```
