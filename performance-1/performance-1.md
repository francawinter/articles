# Thoughts about performance of CSS transitions

## Contents
- what are css transitions 🟡
- why care? 🟡
    - personal regard -> tell a story!
- how to implement? 🔴
- Bonus: JS performance 🔴
- conclusion 🔴

## Intro: Why use animation on a website?

- One of the differences between a website and a book is that you can not only read a website, but also interact with it.
- We can build a interactive website without animations and it will be perfectly fine. Wikipedia, for example, barely uses animation.
- But, with animation, we can improve User Experience (UX) of a website.
    - we can decide to animate these interactions so that feel a little bit more natural and intuitive to use. (needs example)

- As a frontend developer, there are many different ways to animate elements. You can animate with JS, but, if possible, use CSS (why?). (Law of simplest technology) You can get a long way with CSS transitions and keyframes. Personally, I almost never need to use anything else at work.

## What are CSS transitions?
- CSS transitions are the easiest form of animation. You have an element with a state A that turns to state B.
    - Think about a button that changes it's color on hover.
    - With one line of code, you can change the feeling of the interaction completely.
- you might have seen code like this before:

```css
.button {
	background-color: blue;
	color: white;
	transition: background-color 200ms, color 200ms;
}

.button:hover {
	background-color: white;
	color: blue;
}
```
Codepen: https://codepen.io/franca_/pen/xxRJozm?editors=1100

TODO: Improve real code example...

- BUT – every animation comes at a cost. The browser has to *work* to make animations happen. That's why Wikipedia is so fast - the browser doesn't have much to do.

## Why care about performance of CSS transitions? My Story
- started professional frontend development
- happily ever after used `transition: all` (for lazy people)
- one day, a frontend dev specialized on performance saw my code and told me to NEVER use `transition: all`. It would be bad for performance.
- I started to research deeper into the performance of transtions
    - heard about rendering, CPU and GPU before, but:
        - quickly gave up on this
        - I don't regret it: it's a giant rabbit hole.
    - but THIS time, years later, I cared more: A performant page needs less rendering = less energy consumption. 
        - so even if a page feels fast enough, it's still a good idea to care about performance.
- I won't dive into the technical aspect of browser rendering because it would really go beyond the scope of this article.
    - If you're interested, I recommend you the article series by Mariko Kosaka who works at Goole on Chrome. She's a truly inspiring woman, so you should check her out.
    - After my research, I recommend the following:

<br>
<br>

**Safe bets for animation: opacity and transform**

<br>
<br>

## What's so different about opacity and transform?

- they only cause the browser to re-render *once*
- both can be used as animation "hacks"
    - they *seem* to animate the element, but in reality it's a fake animation

### opacity
- the effect is already there from the beginning, only revealed on transtion
    - because of that, browser doesn't have to re-paint everything

### transform
- the element *seems* to be moving, but it's not *really* moving
    - layout doesn't change at all
    - because of that, layout doesn't have to be re-painted


---
## Real-world implementation

This sounds grat in theory, but how do you animate with opacity and transform *only* ? Here's a real world example: A sticky header.

### Our requirements
- On scroll, the header has to be sticky but reduce its height to leave more space for the page content
- A subtle shadow appears on scroll to delimit navigation from content

### First version: brute force
- animate CSS `height` or `padding` property from hardcoded value x to x - n.
- animate CSS `box-shadow` from 0 to x.

#### Brute force code example
Codepen: https://codepen.io/franca_/pen/MWbQQar

The important part, simplified:
```css
.header {
    padding: 30px;
	transition: padding 300s, box-shadow 300s;
}

/* Same HTML element, but class added with JS on scroll */
.header--scrolling { 
    padding: 10px;
    box-shadow: 0 8px 40px 0 gray;
}
```

#### What happens behind the scences?

- Every frame, the browser's GPU (graphics processing unit) needs to render the transition's new state:

[[ GPU visualization ]] ✅

[[ GPU Video]] ✅

### Second version: optimized for performance ✨

Codepen: https://codepen.io/franca_/pen/yLVvvgv

#### First step: box-shadow

Initial situation: A transparent ::before element with a box-shadow ist placed just at the same place the header sits.
```css
.header {
    ...
}

.header::before {
	content: " ";
	position: absolute;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	opacity: 0; /* Hidden by default. */
	box-shadow: 0 8px 40px 0 gray; /* 👈 Shadow! */
}
```

We can then "fake animate" the box-shadow by simply setting the ::before element's opacity to 1;

[[Visualization of ::before element ]] ✅

```css
.header {
    ...
}

.header::before {
	...
	opacity: 0;
	box-shadow: 0 8px 40px 0 gray;
	transition: opacity 300s;
}

.header--scrolling::before {
	opacity: 1; /* ✨ Reveal box shadow on scroll ✨ */
}
```

#### Second step: height

This one is a little tricky. You're lucky if you can just `scale` your header, but the header's content would be scaled as well. But, we can use the `transform` property to shift the header a little more to the top. Then, we have to shift *down* the header's content a little so that it still sits at the center.

[[Visualization of header shifting]] ✅

- on scroll, header is shifted upwards
- on scroll, nav (which is header's content) is shifted a little bit downwards to be centered again

```css
.header {
    padding: 30px;
}

.header--scrolling { 
    transform: translateY(-20px);
}

.header--scrolling .nav {
    transform: translateY(10px);
}
```

In the last step, we animate the `transform` of header and nav:
```css
.header {
    padding: 30px;
    transition: transform 300s; /* Smooth transition upwards */
}

.header--scrolling { 
    transform: translateY(-20px);
}

.nav {
	transition: transform 300s; /* Smooth transition downwards */
}

.header--scrolling .nav {
    transform: translateY(10px);
}
```



