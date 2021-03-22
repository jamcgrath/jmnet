---
title: Positioning the underline in text with CSS
date: "2021-03-22"
thumb_img_path:
content_img_path:
alt_text:
template: post
excerpt: There is a handy CSS rule that can adjust the position of the underline for text

---

Here's 2 ways to position the underline in text. The easiest way is to use `text-underline-offset`.
Another way is to put the text in a `<span>` or `<div>` and use `padding-bottom` and `border-bottom`. Depending on whether text needs to be inline or not the `<span>` or `<div>` will need to have `position` of ` inline-block` or `block`;

<p class="codepen" data-height="493" data-theme-id="32872" data-default-tab="css,result" data-user="jamcgrath" data-slug-hash="gOgYRjY" style="height: 493px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="2 ways to adjust the underline of text">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/gOgYRjY">
  2 ways to adjust the underline of text</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>


<script src="https://cdn.jsdelivr.net/gh/ireade/caniuse-embed/public/caniuse-embed.min.js"></script>
<p class="ciu_embed" data-feature="mdn-css__properties__text-underline-offset" data-periods="future_1,current,past_1,past_2" data-accessible-colours="true">
<p>Data on support for the mdn-css__properties__text-underline-offset feature across the major browsers</p>
</p>