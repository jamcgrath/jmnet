---
title: Convert an accessible hamburger button to vue
date: "2020-04-18"
thumb_img_path: images/convert-hamburglar.jpg
content_img_path:
alt_text:
template: post
excerpt: Let's fork an accessible hamburger button on codepen and use it in Vue.
---

Today let's see how we can refactor an accessible hamburger button using Vue.

The first thing is to fork <a href="https://codepen.io/samikeijonen/pen/jqvxdL">Simple and accessible SVG menu hamburger animation</a> in codepen.

Next let's setup up Vue in codepen.

In the settings go to JS and search for "vue".

<img src="/images/codepen-vue-setting1.jpg" alt  />

Then delete delete `min` from the the vue file name. By doing this Vue devtools will work when the pen is viewed in debug mode.

<img src="/images/codepen-vue-setting2.png" alt />

Next in the Javascript pane add

```js
new Vue({
  el: "#app",
  data: {},
});
```

In the HTML pane add

```HTML

<div id="app"></div>

```

Vue is now setup in our pen.

Now it's time to copy the HTML and CSS from the forked codepen to the Vue codepen. The js section is not needed because Vue will handle all of that.

After copying the HTML and CSS add a boolean to the `data` object in the Javascript panel. Let's call it `toggleButton` and assign it a value of `false`.

```js
new Vue({
  el: "#app",
  data: {
    toggleButton: false,
  },
});
```

Next we will add a click event to the `button` and bind `class` and `aria-expanded` to the `toggleButton` boolean in `data`.

On the button do the following

1.  add `v-on:click="toggleButton = !toggleButton` to change the value between `true` and `false` when the button is pressed.
2.  change `aria-expanded="false"` to `v-bind:aria-expanded="toggleButton ? 'true' : 'false'`. The reason for the ternary is that a boolean value of `false` is used, the markup on the button will be `aria-expanded=` instead `aria-expanded="false"`.
3.  bind a `class` attribute to the button by adding `v-on:class="{'opened' : toggleButton}"`. Vue will automatically merge the two `class` on the button together.

The `button should look like the following:

```HTML

 <button
    class="menu-toggle"
    :class="{'opened': toggleButton}"
    id="menu-toggle"
    :aria-expanded="toggleButton ? 'true' : 'false'"
    @click="toggleButton = !toggleButton"
  >...</button>

```

That's it. Now the button function like the codepen that it was forked from. Here's a working example.

<p class="codepen" data-height="300" data-theme-id="32872" data-default-tab="result" data-user="jamcgrath" data-slug-hash="BaozQwq" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Accessible Hamburger Vue">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/BaozQwq">
  Accessible Hamburger Vue</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
