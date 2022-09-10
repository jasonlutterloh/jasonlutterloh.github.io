---
layout: post
title: "How to add a Service Worker to your Progressive Web App (PWA) using Workbox and Rollup"
date: 2020-08-08 00:00:00 -0500
author: Jason Lutterloh
image: /assets/posts/post_workbox.png
excerpt: "This guide will provide a super simple approach to service workers in a project bundled with Rollup (but could easily be applied to other bundlers as well)."
canonical: https://lutterloh.dev/posts/2020-08-08-service-worker-pwa-workbox-rollup/
---

Recently, I converted one of my existing web apps into a PWA so that I could "install" it on my device and run it offline. I spent far too long researching how to properly add a service worker and found that for simple apps, most documentation is far too detailed. For a simple app, creating a service worker was actually pretty easy.

This guide will provide a super simple approach to service workers in a project bundled with Rollup (but could easily be applied to other bundlers as well).

Context to be aware of:

- This guide assumes you know something about PWAs and have already written your manifest file
- This guide assumes your application is bundled with Rollup
- The application used as an example in this guide is pretty simple. It's basically JavaScript running some analysis on a user's data input and printing out some pretty charts. There are no external service calls to be worried about and no images to load.
- This guide relies on using Workbox to create the service worker (as recommended by [web.dev](https://web.dev/service-worker/)) but it is entirely possible to create one from scratch.

### Step 1: Install the Workbox Rollup Plugin

This will install the package that runs to generate your service worker.

```bash
npm install rollup-plugin-workbox
```

### Step 2: Add the generation step to your Rollup config\*\*

Add the `generateSW` call to your `rollup.config.js` file after all the other steps and plugins. You want the service worker to be generated after you've already bundled your files.
The configuration object tells the plugin where to generate the service worker, what kind of files to cache, and allows for other configuration options.

The main points to note are:

- `swDest`: where to generate the service worker and what to name the file (this should be at the root of your build/public folder)
- `globDirectory`: what directory to search for files to cache on bundle
- `globPatterns`: what file types to tell the service worker to cache
- `skipWaiting`/`clientsClaim`: in a nutshell, force the worker to update things quicker

You can read more about the configuration options at the [Workbox Reference](https://developers.google.com/web/tools/workbox/reference-docs/latest/module-workbox-build#.generateSW).

```javascript
// The majority of this code was copied from the official Workbox documentation
import { generateSW } from 'rollup-plugin-workbox';
//...
generateSW({
    swDest: 'public/sw.js',
    globDirectory: 'public/',
    globPatterns: [
        '**/*.{html,json,js,css}',
    ],
    skipWaiting: true,
    clientsClaim: true,
    runtimeCaching: [{
        urlPattern: /\.(?:png|jpg|jpeg|svg)$/,
        handler: 'CacheFirst',
        options: {
            cacheName: 'images',
            expiration: {
                maxEntries: 10,
            },
        },
    }],
}),
```

### Step 3: Link Your Service Worker to Your Web Page

The last step enables having your web page tell your browser that a service worker is present and should be registered. Do this in your main `.js` file. Make sure that your filename and path to the service worker match what you configured in Step 2.

```javascript
if ("serviceWorker" in navigator) {
  // Use the window load event to keep the page load performant
  window.addEventListener("load", () => {
    navigator.serviceWorker.register("/sw.js");
  });
}
```

### Step 4: Run Your Script and Test It Out

```bash
npm run build
```

### Step 5: (Optional) Fine-tune Approach

When you run your build, four files will be created. You'll want them on your server but not necessarily in your git project so add this to your `.gitignore`.

```plaintext
# Service Worker
**/workbox*
**/sw*
```

Also, you should configure your host to not cache your service worker. If you use firebase hosting, just add this to your `firebase.json`:

```json
{
  "hosting": {
  //...,
    "headers": [{
      "source" : "/sw.js",
      "headers" : [{
        "key" : "Cache-Control",
        "value" : "no-cache"
      }]
    }],
  //...
```

There's a lot more detail in the official documentation but hopefully this gets your started. Good luck!

Sources:

- [Workbox](https://developers.google.com/web/tools/workbox)
- [Workbox Rollup Plugin](https://www.npmjs.com/package/rollup-plugin-workbox)
