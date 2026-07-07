# PERSONAL DRUMKIT PROJECT

This project was made by completing Day 1 of the [30 Days JavaScript Challenge](https://javascript30.com/).

## Table of contents

- [Overview](#overview)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [AI Collaboration](#ai-collaboration)
- [Author](#author)

## Overview

### Screenshot

![Site](DrumKitSite.png)

### Links

- Live Site: [Here](https://zzzylo.github.io/Drumkit-/)

## My process

This is my very first JavaScript project. It was confusing at first, but I was already familiar with the fundamentals — functions, objects, and variables — so I had a starting point to build from.

**1. Listening for key presses**

I started with an event listener on the `window` to detect when a key is pressed, using the `keydown` event.

```js
window.addEventListener("keydown", play);
```

**2. Matching the key to its sound**

The `play` function handles the actual logic. Each `<audio>` element and each `.key` div has a matching `data-key` attribute set to a keycode. I used an attribute selector in the query to find the exact audio and div that match whichever key was pressed. Before playing, `audio.currentTime = 0` resets the sound to the beginning — this makes sure that pressing the same key rapidly always restarts the sound instead of overlapping or ignoring the press. Finally, I add a `"playing"` class to the matching div, which triggers a CSS transition for the visual press effect.

```js
function play(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  audio.currentTime = 0;
  audio.play();
  key.classList.add("playing");
}
```

**3. Cleaning up after the animation**

Adding the `"playing"` class is only half the job — if it's never removed, the animation won't replay on the next press. So in the global scope, I selected all `.key` divs into a single NodeList and used `forEach` to attach a `transitionend` listener to each one.

```js
const keys = document.querySelectorAll(".key");
keys.forEach((key) => key.addEventListener("transitionend", removeTransition));
```

Then I wrote the `removeTransition` function, which removes the `"playing"` class once the CSS transition finishes.

```js
function removeTransition(e) {
  if (e.propertyName !== "transform") return;
  this.classList.remove("playing");
}
```

### Built with

- HTML5 markup
- CSS custom properties
- Flexbox / Grid
- Plain JavaScript

### What I learned

This project taught me how JavaScript actually connects to the DOM in practice, rather than in isolated exercises:

- **`data-*` attributes** are custom attributes I can define myself, and are best used for storing structured _data_ (like an ID) rather than styling — as opposed to `class`, which is meant for grouping elements for CSS/JS styling purposes.
- **Dot notation** always means the same thing — accessing a property on an object — regardless of whether that property holds a plain value or a function. Methods (like `.play()` or `.classList.add()`) are just properties whose value happens to be a function.
- **HTML elements are objects**, and different tags come with different built-in methods depending on what "type" of element they are. An `<audio>` element gets `.play()` and `.currentTime` because it's a media element, while a `<h2>` does not — because those methods live on `HTMLMediaElement`, not the shared `HTMLElement` base that all tags inherit from.
- **The prototype chain** is the mechanism behind this: if JavaScript can't find a property directly on an object, it looks up through that object's "parent" blueprints until it finds it or runs out.
- **`transitionend`** fires automatically once a CSS transition finishes, and fires once _per property_ if multiple properties are transitioning at once. Checking `e.propertyName` prevents the cleanup logic from running multiple times unnecessarily.

### AI Collaboration

- Used **Claude** as a guide throughout this project — asking questions about _why_ the code worked the way it did (data attributes vs. classes, prototype chains, event objects) rather than just copying the solution, and for help structuring the page layout.

## Author

- Website - [here](https://zzzylo.github.io/Drumkit-/)
- Frontend Mentor - [Zzzylo](https://www.frontendmentor.io/profile/Zzzylo)
- Github - [Zzzylo](https://github.com/Zzzylo)
