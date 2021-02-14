---
layout: post
title: "Making API Calls Within a Svelte App"
date: 2021-02-13 00:00:00 -0500
author: Jason Lutterloh
excerpt_separator: <!--more-->
image: /assets/posts/post_apisvelte.png
---

There's plenty of ways to do make API calls from within a Svelte app but I'd like to share the approach that's worked for me.

<!--more-->

Demo:  [Svelte REPL - Demo](https://svelte.dev/repl/cb31be94ea444b41a11d1320d16ba6dc?version=3.32.3)

## Prerequisites

First things first, start a new Svelte app. Check out [Svelte's official Getting Started guide](https://svelte.dev/blog/the-easiest-way-to-get-started#2_Use_degit) for that.

## Getting Started

This tutorial will walk you through the hypothetical use case of calling an API to get a list of whiskey cocktails and displaying them. The data we're going to be working with will be in the following format:

<sub>Free API provided by [TheCocktailDB](https://www.thecocktaildb.com)</sub>

```json
{
  "drinks":[
    {"strDrink":"Allegheny","strDrinkThumb":"https:\/\/www.thecocktaildb.com\/images\/media\/drink\/uwvyts1483387934.jpg","idDrink":"11021"},
    {"strDrink":"Bourbon Sour","strDrinkThumb":"https:\/\/www.thecocktaildb.com\/images\/media\/drink\/dms3io1504366318.jpg","idDrink":"11147"},
    {"strDrink":"John Collins","strDrinkThumb":"https:\/\/www.thecocktaildb.com\/images\/media\/drink\/0t4bv71606854479.jpg","idDrink":"11580"},
  ]
}
```

### Step 1: Create Your Data Store

Okay, within your new app, create a new file inside your `src` folder entitled `store.js`. This is where you'll "store" the data you pull from your API as well as do any data transformation.

Once you've created `store.js`, add the following code:

```javascript
import { writable, derived } from 'svelte/store';

/** Store for your data. 
This assumes the data you're pulling back will be an array.
If it's going to be an object, default this to an empty object.
**/
export const apiData = writable([]);

/** Data transformation.
For our use case, we only care about the drink names, not the other information.
Here, we'll create a derived store to hold the drink names.
**/
export const drinkNames = derived(apiData, ($apiData) => {
  if ($apiData.drinks){
    // Create a new array of just drink names
    return $apiData.drinks.map(drink => drink.strDrink); 
  }
  return []; // Default to empty array
});
```

### Step 2: Make Your API Call

Inside `App.svelte` is where we'll actually make the API call. Technically, you can do this in any of your Svelte files, but for this tutorial's purpose we'll use this.

Replace everything inside the `<script>` tag with the following:

```javascript
import { onMount } from "svelte";
import { apiData, drinkNames } from './store.js';

// When the page is loaded, make your API call
onMount(async () => {
  // Make your API call
  fetch("https://www.thecocktaildb.com/api/json/v1/1/search.php?i=bourbon")
  .then(response => {
    // Parse response as json
    return response.json()
  })
  .then(data => {
    // Console logging for debug purposes
    console.log("Data", data);
    // Save data to store
    apiData.set(data); 
  }).catch(error => {
    // Do error handling
    console.error("Error", error);
    return [];
  });
});
```

### Step 3: Display Your Data

Now that we've saved and transformed the data in the store, we can call the store to get and display our data. Within the same `App.svelte` file we added the API call to, replace the code within `<main>` with the following:

```html
<h1>Whiskey Drinks Menu</h1>
<ul>
<!-- For each drink inside our derived store, create a list item -->
{#each $drinkNames as drinkName}
  <li>{drinkName}</li>
{/each}
</ul>
```

_Voila!_ Pretty simple, right? With this tutorial, you made an API call, did some data transformation, and displayed it! Obviously, this is a super simple use case, but hopefully this can used as a building block in your apps going forward. Thanks for reading and good luck!

See it in action here: [Svelte REPL - Demo](https://svelte.dev/repl/cb31be94ea444b41a11d1320d16ba6dc?version=3.32.3)