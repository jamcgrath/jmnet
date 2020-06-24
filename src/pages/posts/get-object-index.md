---
title: Find an item in an array of objects
date: "2020-05-17"
thumb_img_path: images/findindexofobjectinarray.jpg
content_img_path:
alt_text:
template: post
excerpt: Let's play with array.find, array.indexOf and the rest operator
---

Let's look at how to find an item in an array of objects if we know one of the object's properties.

In the following code example we use the `Array.find()` to search for the object with the property that is known and assign that object to a variable. Using `Array.indexOf()` to find the index of the object that we are looking for.

```
  const arrayOfObjects =  [
    {id: 123},
    {id: 43},
    {id: 8999},
    {id: 12},
    {id: 245}
  ]

  const theObject = arrayOfObjects.find(obj => obj.id === 12);
  const indexOfTheObject = arrayOfObjects.indexOf(theObject);

  console.log(theObject); // { id:12 }
  console.log(indexOfTheObject); // 3

```

Now that we found the index of our object let do something with it.

Let's assign the object name and nickname properties. Using dot notation we can add `name: "William"`. Next we will overwrite all the properties in the object we searched for using the spread operator. While doing we can add on nickname too. If nickname already existed in the object it would be overwritten with `nickname: Bill`.

```
  theObject.name = "William";

  arrayOfObjects[indexOfTheObject] = {...theObject, nickname: 'Bill'};
  console.log(arrayOfObjects);
}
```
