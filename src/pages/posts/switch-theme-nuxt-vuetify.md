---
title: Switch to user preferred color scheme in Nuxt and Vuetify
date: "2021-07-02"
template: post
excerpt: Automatically switch the website theme with Nuxt.js and Vuetify.js
---

One of the projects I have been working on lately uses Nuxt and Vuetify. Someone on the team decided that dark mode is the preferred color scheme for the website. Personally I'm not a fan of the dark mode because I find it more eye fatiguing. To solve my personal issue I decided to make Nuxt and Vuetify automatically switch the color scheme based off the users preferred preference in their device settings. 

According to the [Vuetify Docmentation]([https://vuetifyjs.com/en/features/theme/#light-and-dark](https://vuetifyjs.com/en/features/theme/#light-and-dark)), there is a global variable that can be changed to switch the theme.

In `layouts/default.vue` I put in the following code. 

```jsx

beforeMount () {
    //check if browser supports dark mode.
    if (window.matchMedia && window.matchMedia('(prefers-color-scheme)').media !== 'not all') {
     
			//if user prefers light mode switch to light mode
      if(window.matchMedia('(prefers-color-scheme: light)').matches) {
        this.$vuetify.theme.isDark = false;
      }
    }
  },
```

---

A couple of notes on the code above. 

1. The choice of nesting the if statements was for readability.  There are couple of other ways this could have could have combined all the if statements in to one or done a giant ternary. Personally I like the ternary for some reason. 
2. The reason the first if has `'not at all'` is because it is just checking to see that `prefers-color-scheme` exists in the window. The value is not that important at point if the code. 

```jsx
if(
	window.matchMedia &&
	window.matchMedia('(prefers-color-scheme)'.media !== 'not at all') &&
	window.matchMedia('(prefers-color-scheme: light)')) {
			 this.$vuetify.theme.isDark = false;
}

 this.$vuetify.theme.isDark = window.matchMedia && 
 window.matchMedia('(prefers-color-scheme)'.media !== 'not at all') &&
 window.matchMedia('(prefers-color-scheme: light)') ? false : true;
```