# Thoughts about performance of CSS transitions

## Contents
- what are css transitions
- why care?
    - personal regard -> tell a story!
- how to implement?
- Bonus
- conclusion

## Intro: Why use animation on a website?

- One of the differents between a website and a book is that you can not only read a website, but also interact with it.
- We can build a interactive website without animations and it will be perfectly fine. Wikipedia, for example, barely uses animation.
- But, with animation, we can improve User Experience (UX) of a website.
    - we can decide to animate these interactions so that feel a little bit more natural and intuitive to use. (needs example)

- As a frontend developer, there are many different ways to animate elements. You can animate with JS, but, if possible, use CSS (why?). You can get a long way with CSS transitions and keyframes. Personally, I almost never need to use anything else at work.

## What are CSS transitions?
- CSS transitions are the easiest form of animation. You have an element with a state A that turns to state B.
    - Think about a button that changes it's color slightly on hover.
    - With one line of code, you can change the feeling of the interaction completely.
- you might have seen code like this before:

```css
.button {
    color: black;
    transition: 200ms background-color; /* smooth color animation! */
}
.button:hover {
    color: gray;
}
```
TODO: real code example...

- BUT – every animation comes at a cost. The browser has to *work* to make animations happen. That's why Wikipedia is so fast - the browser doesn't have much to do.

## Why care about performance of CSS transitions? My Story
- started professional frontend development
- happily ever after used `transition: all` (for lazy people)
- one day, a frontend dev specialized on performance saw my code and told me to NEVER use `transition: all`. It can be bad for performance.
- I started to research deeper into the performance of transtions
    - heard about rendering, CPU and GPU before, but:
        - quickly gave up on this
        - I don't regret it: it's a giant rabbit hole.
    - but THIS time, years later, I cared more: A performant page needs less rendering = less energy consumption.
- I won't dive into the technical aspect of browser rendering because it would really go beyond the scope of this article.
    - If you're interested, I recommend you the article series by Mariko Kosaka who works at Goole on Chrome. She's a truly inspiring woman, so you should check her out.
    - After my research, I recommend the following:

<br>
<br>

**Safe bets for animation: opacity and transform**

<br>
<br>

## What's different for opacity and transform?

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

