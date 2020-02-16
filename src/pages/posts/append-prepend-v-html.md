---
title: Prepend / Append to v-html in VUE
date: "2020-02-09"
thumb_img_path: images/append-v-html.png
content_img_path:
alt_text:
template: post
excerpt: It never occured to me that you can add things to v-html
---

In the thing I'm currently working on at Mamamia, the content for the page is coming from a WYSIWYG editor. The section of the page where it appears has a title that is planned to be hardcoded in to the markup. I didn't want to add an extra `div` just to display the content of the `v-html`. It occured to me that I could easily append or prepend additional markup to it in the Vue template. However it appears that this can't be done with `v-text`. The codepen below also uses this technique.

```

<div v-html="`<h2>My Cool H2 Title</h2>${wysiwyg_data_from_api}`></div>"

```

<p class="codepen" data-height="973" data-theme-id="32872" data-default-tab="result" data-user="jamcgrath" data-slug-hash="WNvrqpB" style="height: 973px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Append &amp;amp; Prepend to v-html ">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/WNvrqpB">
  Append &amp; Prepend to v-html </a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
