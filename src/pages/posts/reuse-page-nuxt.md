---
title: Reusing pages in different routes in Nuxt
date: "2021-03-09"
thumb_img_path: 
content_img_path:
alt_text:
template: post
excerpt: Have you ever found yourself having multiple routes that are not related use the same design? Here's a way to reuse the page in a different route. 

---

# Reusing pages in different routes in Nuxt

Say you got this design and it's exactly the same for different routes. A real world example of this is when we implemented AMP on mamamia.com.au. The only difference between the AMP and non-AMP pages was the `amp-img` component. It was decided that we were going to reuse the page in both routes and just conditionaly load the `amp-img` component depending on the route. 

Our directory structure looked someting like this

```
/pages
  /_page
  	/amp
```

We felt it was best to find a way to use the same template for both routes. Our biggest concern was maintaining two files that are practically Identical. Our solution was to use one file in the `/_page` directory and the `/amp` route would import the file and display it. 

This is what is in  `/_page/amp/index.vue`.

```
<script>
import index from "~/pages/_page/index.vue"
export default index

</script>
```
