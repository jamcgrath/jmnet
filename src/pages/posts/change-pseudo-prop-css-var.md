---
title: Changing pseudo-elements with CSS Custom Properties
date: "2020-02-02"
thumb_img_path: images/hover-wtf.png
content_img_path:
alt_text:
template: post
excerpt: Did you know there are 2 ways to dynamically change the CSS properties of pseudo-elements?
---

As far as I know, there wasn't any way to dynamically change the CSS properties of pseudo-elements. Now that CSS custom properties are supported in the latest browsers, there are two ways in which this can be done. The following codepen demonstrates it.

<p class="codepen" data-height="407" data-theme-id="32872" data-default-tab="presult" data-user="jamcgrath" data-slug-hash="dyPELwL" style="height: 407px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title=" Change pseudo element css with css custom properties">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/dyPELwL">
   Change pseudo element css with css custom properties</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

The first way is so to set the pseudo-elements value globally and then modify the global custom property in the `:root`.

```

:root {
	--global-css-var: yellow;
}

a:hover {
	color: var(--global-css-var);
}

```

This is how to modify the `:root` the style needs to change on the `documentElement`.

```

document.documentElement.style.setProperty('--global-css-var', 'green' );

```

The other way to change the pseudo-element property is to set the custom property locally.

```

a {
	--local-css-var: purple;

	color: black;
}

a:hover {
	color: var(--local-css-var);
}


```

To change the `:hover` color, change the custom property of the `<a>`;

```

const links = document.querySelectorAll('a');
links.forEach(link => {
	link.style.setProperty('--local-css-var', 'magenta');
});

```

Between the two methods, the first way of changing the custom property globally is better because it doesn't loop through a list of elements.
