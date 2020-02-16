---
title: Persistent Font Resizer with vanilla JS
excerpt: >-
  Let's look at how I made this font resizer using vanilla JS, session storage and CSS custom properties.
date: "2019-11-04"
thumb_img_path: images/persistent-font-resize.png
content_img_path:
alt_text: "Screenshot of code"
template: post
---

<p class="codepen" data-height="300" data-theme-id="32872" data-default-tab="result" data-user="jamcgrath" data-slug-hash="bGbyYze" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Font Resizer Updated">
  <span>See the Pen <a href="https://codepen.io/jamcgrath/pen/bGbyYze">
  Font Resizer Updated</a> by James (<a href="https://codepen.io/jamcgrath">@jamcgrath</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

Several years ago I was tasked with making a font resize function for a website I was working on. At that time I made it in jQuery. That version can be seen on codpen[Font Resizer](https://codepen.io/jamcgrath/pen/GgzqqY)

I decided to fork, refactor and update the font resize pen to not depend on jQuery and to use the latest in CSS and JS.

The first thing to do is setup the HTML and CSS (copied straight from codepen)

```html
<div class="wrap">
  <p class="font-changer">
    <b>FONT SIZE:</b><button class="js-font-decrease">-5%</button>
    <button class="js-font-increase">+5%</button>
  </p>

  <h2>Change the font size then refresh the page</h2>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto totam minus
    voluptates consectetur doloribus beatae, asperiores, eaque ipsa perspiciatis
    dolores voluptate esse magni quisquam dolorum maxime ab molestiae dolor
    dicta. Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque eum
    necessitatibus fugiat veritatis veniam in, numquam perferendis nobis
    possimus illo eos consectetur ipsa quibusdam? Amet id praesentium aperiam
    similique sit.
  </p>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto totam minus
    voluptates consectetur doloribus beatae, asperiores, eaque ipsa perspiciatis
    dolores voluptate esse magni quisquam dolorum maxime ab molestiae dolor
    dicta.
  </p>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto totam minus
    voluptates consectetur doloribus beatae, asperiores, eaque ipsa perspiciatis
    dolores voluptate esse magni quisquam dolorum maxime ab molestiae dolor
    dicta.
  </p>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit. Iusto totam minus
    voluptates consectetur doloribus beatae, asperiores, eaque ipsa perspiciatis
    dolores voluptate esse magni quisquam dolorum maxime ab molestiae dolor
    dicta.
  </p>
</div>
```

In the original version of this I used `<span>` instead of `<button>` as the clickable element to trigger the font size change. Using `<button>` makes much more sense to me. I like to follow the rule that if the thing you are clicking does some kind of interaction then it should be a `<button>`. With buttons we get a lot for free.

- In a form it can reset or submit form data
- Announced as an interactive control by screen readers
- Receive keyboard focus by default
- Be disabled with the `disabled` attribute
- Show `:focus`, `:hover`, `:active`, `:disabled`

```css
:root {
  --fontSize: 100%;
}

body {
  font-size: var(--fontSize);
  padding: 1em;
}

.wrap {
  width: 40em;
  margin: 0 auto;
}

b {
  margin-right: 1em;
}

p {
  line-height: 1.5;
}

button {
  padding: 0.5em;
}
```

Next thing to do is to implement the JS to handle the font resizing and session persistence.

First, select the `<body>`, and the `<buttons>` and assign them to variables

```javascript
const body = document.querySelector("body");
const increaseButton = document.querySelector(".js-font-increase");
const decreaseButton = document.querySelector(".js-font-decrease");
```

Next up is make a two named anonymous function called `currentFontSize` that will get the current `font-size` from the CSS custom property used on the `<body>` and `sessionFontSize` that will get the data in the browsers sessions storage whatever size we pass to it.

Be sure to note that when using `getComputedStyle(…).getPropertyValue(…)`the data returned is a string. It’s wrapped in the `parseInt()` function because it needs to be a number when it is used later on in the code.

```javascript
const currentFontSize = () =>
  parseInt(getComputedStyle(body).getPropertyValue("--fontSize"));

const sessionFontSize = size => sessionStorage.setItem("fontSize", size);
```

Next create event listeners for the buttons that will increase or decrease the font size by 5%. The two event listener functions are almost identical. They call `currentFontSize` and then either add or subtract a value of 5. Then it sets the CSS custom property on the `<body>`. Then write the new font size to the browsers session storage.

`body.style.setProperty()` is passed two parameters that are strings. The first parameter is the CSS custom property that will be modified and the value. The second parameter is using interpolation to create a percentage by using javascript template literals ( `` `${newFontSize}%` ``)

```javascript
increaseButton.addEventListener("click", () => {
  const newFontSize = currentFontSize() + 5;
  body.style.setProperty("--fontSize", `${newFontSize}%`);
  sessionFontSize(newFontSize);
});

decreaseButton.addEventListener("click", () => {
  const newFontSize = currentFontSize() - 5;
  body.style.setProperty("--fontSize", `${newFontSize}%`);
  sessionFontSize(newFontSize);
});
```

The last thing to do is create one more event listener for `DOMContentLoaded` that will check session storage to see if there is a size there and then set the font size on the `<body>`.

```javascript
document.addEventListener(
  "DOMContentLoaded",
  () => {
    if (sessionStorage.fontSize) {
      body.style.setProperty(
        "--fontSize",
        `${sessionStorage.getItem("fontSize")}%`
      );
    }
  },
  false
);
```

The full javascript section in the codepen looks like this.

```javascript
const body = document.querySelector("body");
const increaseButton = document.querySelector(".js-font-increase");
const decreaseButton = document.querySelector(".js-font-decrease");

const currentFontSize = () =>
  parseInt(getComputedStyle(body).getPropertyValue("--fontSize"));

const sessionFontSize = size => sessionStorage.setItem("fontSize", size);

increaseButton.addEventListener("click", event => {
  const newFontSize = currentFontSize() + 5;
  body.style.setProperty("--fontSize", `${newFontSize}%`);
  sessionFontSize(newFontSize);
});

decreaseButton.addEventListener("click", event => {
  const newFontSize = currentFontSize() - 5;
  body.style.setProperty("--fontSize", `${newFontSize}%`);
  sessionFontSize(newFontSize);
});

// change fontsize if there is a size in storage & when dom is ready
document.addEventListener(
  "DOMContentLoaded",
  () => {
    if (sessionStorage.fontSize) {
      body.style.setProperty(
        "--fontSize",
        `${sessionStorage.getItem("fontSize")}%`
      );
    }
  },
  false
);
```

There are a couple of issues to note about the code above. First, it doesn’t work in older browsers that don’t support CSS custom properties. If older browser support is a requirement then I would suggest changing the js to use the older es5 syntax and css that has a fallback for the CSS custom properties.
