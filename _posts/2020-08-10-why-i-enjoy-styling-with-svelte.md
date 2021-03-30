---
layout: post
title: "Why I Enjoy Styling With Svelte"
date: 2020-07-10 00:00:00 -0500
author: Jason Lutterloh
excerpt: "Svelte is the perfect fit I was looking for and I'll explain why."
image: /assets/posts/post_svelte.png
---

I started using Svelte a couple of months ago for my [Peloton Metrics](https://github.com/jasonlutterloh/metrics-peloton) project with the promise that it would lead to a simple development process. I’ve used React in the past for enterprise-level applications but it always seemed like overkill for what I was doing in my spare time and I never liked how it handled styling. Svelte is the perfect fit I was looking for and I'll explain why.

First, a little context...

My early front-end developer years were consumed with creating perfectly reusable, performant CSS classes with inheritance and flexibility in mind. This was before preprocessors or variables or complicated build scripts. I wrote everything by hand. I never used a tag or ID in my selectors unless I had to and inline styles were a non-starter. Tag selectors weren’t performant, IDs were for javascript, and inline styles were for people who were too lazy to create a new CSS file and link it.

Anyways, back to now...

When I started using Svelte a couple months ago, I was enamored with the idea that all of a component’s code (HTML, Javascript, and CSS) could be contained within one file in a clean, elegant fashion. I’m constantly searching for ways to make my codebase simpler and Svelte offers a way to take what would be three files (HTML, Javascript, and CSS) and put them into one file.

Sure, other frameworks allow for this too. I’ve built a number of React apps that have a similar structure but they always felt kind of wrong and unconventional. React's reliance on inline styles, camelCase class names, and lots of brackets always felt unnatural and counter to everything I’ve learned. For this (and a few other reasons), I’ve never really liked it and especially not for smaller apps.

With Svelte, I decided to go all-in and try out what it had to offer out of the box. If you aren't familiar, a Svelte component takes on the following structure:

```html
<script>
  let name = 'world';
</script>

<h1>Hello {name}!</h1>

<style>
  h1 {
    color: #0000FF
  }
</style>
```

[Svelte REPL](https://svelte.dev/repl/974a0475baeb4ac8ac8a80c34a60445d)

You'll notice a `<script>` section, HTML, and a `<style>` section. All of this should look pretty familiar. One of my favorite things about Svelte is it doesn't require you to learn a new way of writing code. You can actually write vanilla front-end code (along with common framework conventions such as brackets, etc).

What sets Svelte apart though is how it handles CSS. Due to how Svelte compiles the app, it will take the CSS written with a tag selector, create a class for you with a unique class name, and assign that class name to the applicable tags in your component. For instance, the above code would be compiled to a CSS selector like:

```css
h1.svelte-rbuihw {
  color: #0000ff;
}
```

alongside HTML that would look like:

```html
<h1 class="svelte-rbuihw">Hello world!</h1>
```

This is how I found myself writing styles with nothing more than HTML tag selectors in my project. I'll admit that, at first, it felt a little jarring to do so but it's led to tutorial-simple CSS alongside readable HTML. I can easily tell exactly what everything does and how it will work together. There are no long strings of class names, inline styles, or worrying about collisions and inheritance.

You may be reading this and giving me a skeptical eyebrow about now. I would too if I was reading this for the first time. You might be asking something like, “That makes sense for a 'Hello World' but that can't work in a real app. What about global styles or styles that you want to reuse across components?” That's a fair question.

Practically, I still have a global CSS file and if I find myself needing a style that can be reused across components, I use it (this works well for certain headings, links, or buttons). You could argue that with enough granular components I wouldn’t need to do this. I could create a component for each level of heading, etc but I’ve always felt super granular levels of components are tedious and not always worth the effort. Life is a balance.

Bottom line: Styling components with Svelte is simple and allows for readability. It requires a little bit of a mind-shift if you're used to doing CSS a certain way but it's definitely made my life easier. It's definitely worth a try on your next small web app.
