# PERSONAL DRUMKIT PROJECT

This project is made by doing the 30 days Javascript Challenge of [Javascript30](https://javascript30.com/)

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

= Live Site: [Here](https://zzzylo.github.io/Drumkit-/)

## My process

This is my very first JS project. It was confusing at first but luckily, I am already familiar with using the fundamentals such as functions, objects, and variables. First, I made an eventListener to listen for key press using 'keydown'.

```js
window.addEventListener("keydown", play);
```

Then, I put a function named "play" as a parameter to process the logic. In this function, each audio element is assigned in the variable audio. To specify which audio element is being selected, I used the attribute selector in css and inside that, selected each by the keycode. The same applies to the key variable. I assigned each divs with the class key to the key variable. the audio.currentTime = 0 resets audio each time this event is trigerred and then played. Finally, I added a class called playing in order for the transition effect to apply.

```js
function play(e) {
  const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
  const key = document.querySelector(`.key[data-key="${e.keyCode}"]`);
  audio.currentTime = 0;
  audio.play();
  key.classList.add("playing");
}
```

After that, in the global scope, I put a variable to store the divs with the class of key in a single nodelist in order to use forEach method so an eventlistener called "transitionend" could apply to each of them.

```js
const keys = document.querySelectorAll(".key");
keys.forEach((key) => key.addEventListener("transitionend", removeTransition));
```

then proceeded to make the function that removes the class playing in each of the divs with key class after the css transition ends.

```js
function removeTransition(e) {
  if (e.propertyName !== "transform") return;
  this.classList.remove("playing");
  console.log(e);
}
```

### Built with

- HTML5 markup
- CSS custom properties
- Flexbox
- Plain JavaScript

### What I learned

### AI Collaboration

- Claude
- As a guide to proper page layout

## Author

- Website - [here](https://zzzylo.github.io/Drumkit-/)
- Frontend Mentor - [Zzzylo](https://www.frontendmentor.io/profile/Zzzylo)
- Github - [Zzzylo](https://github.com/Zzzylo)
