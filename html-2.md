# Hands-on HTML and Why All Programming Languages Look So Cryptic 

## Computers need rules

Computers can read, it's called _parsing_. They read one character after another, like `H-e-l-l-o`. It looks like an elementary student. Most of us have learned reading by hiding the following letters with some piece of paper to not get confused, slowly uncovering letter by letter.

![An elementary student slowly reads a word](https://dev-to-uploads.s3.amazonaws.com/i/01whlnj8lylg2gdh8fxx.png)

We don't want the computer to read everything in the same intonation – there should be headlines, paragraphs, important sections. Even the driest paper needs a line break at some point.

## The HTML language concept

**HTML isn't about the _looks_ of a website, but it helps to structure it, prioritize, divide content into sections.**

To be able to do this, HTML's inventor Tim picked special characters which normally don't occur in texts: angle brackets. Symbols which immediately shut out the non-programmer.

I still remember looking at HTML for the first time and it felt just wrong. Being a designer, it didn't look visually pleasing. It looked *scary*, not *human-readable*. It felt like looking at something that I _was not supposed_ to see, almost like looking at organs inside a human body, which is not far away from the truth. 

```html
<p>Click <a href="#" target="blank">here</a></p>
```

So, why do we need these scary brackets again? To section the content. The browser won't read the brackets as normal text. On the contrary, it will stop and look carefully at the character. For everything the computer isn't supposed to just display but to _interpret_, we need special symbols and keywords. This is the reason for all programming languages looking like somebody just randomly pounded on the keys...


### Rules for the browser #1

- normal letters: continue reading
- numbers: continue reading
- angle bracket: _STOP!!_

It would look like this:

`Hello bla bla bla <` _Oh! Hold on. That's a special character. We aren't supposed to read this out loud._


### Rules for the browser #2

- special character < : Don't read it, start listening. 
- special character > : Ok, continue reading...

Let's try to add a heading to our text.

```
Bla bla bla <Now a heading, please> My glorious heading ✨
```

The browser doesn't really understand English, it reads the characters bluntly one by one. But it knows that angle brackets do have a special meaning and it is not supposed to display them on the page. 

Tim had to think about what to write inside the brackets. How could we label a heading? He decided on `h1` for an important heading: `h` for heading and `1` for important.

![An h1 tag](https://dev-to-uploads.s3.amazonaws.com/i/wrnauxzdiiqffvky2ymk.png)

## The three puzzle pieces of HTML

It's always the same:
1. open the bracket `<`
2. add the abbreviation for the content `h1`
3. close the bracket `>`

The brackets _hug_ the content. You always need them both. It's like a little family: 👩‍👩‍👧

```html
Bla bla bla <h1> My glorious heading ✨
```

`<h1>` won't be read out loud, only what follows afterward.

That's very short. Tim, as every smart person, loves abbreviations. His train of thought is so complex that it needs quick tools in order to not forget his thoughts.

For people that know the English language (like Tim), `h1` is simple to remember. Others have to get used to the fact that the world of programming is based on the English language and western culture. But we can still shape the future, my friends!

Let's look at our heading again. If we continue writing, everything after `h1` will be part of the heading – that's what we told the browser.

Look at the black and white rectangle below. It's a small website preview.

- On the left side, you see the HTML. It's the representation of a .html document.
- On the right side, you find the visual result which is displayed by the browser. It's like an _opened_ .html document.

{% codepen https://codepen.io/franca_/pen/zYvWWOO default-tab=html,result %}

We don't want the paragraph to belong to the heading. Our heading should look more like this: 

```html
Bla bla bla <h1> My glorious heading ✨ <Ok, now STOP IT!> This is a paragraph again.
```

You have to tell the browser in some way to stop thinking everything that follows should be read the same way. Like a good story, it needs a beginning and an end. 

## Almost done! The last step to write valid HTML

As always, the end needed to be nice and short. Tim had the idea to use `h1` again, but this time with a slash `/`: 

![H1 closing tag](https://dev-to-uploads.s3.amazonaws.com/i/gtmtcx8ew1ynl3i1sd22.png)

These brackets and the abbreviations inside it are called **tags**. Don't get confused with the tags on Instagram. `<h1>` is the OG tag, my friend.

Every tag consists of 3 elements, remember the family. 👩‍👩‍👧
To create a heading, you need two of them: 
1. The opening tag `<h1>`
2. The closing tag `</h1>`

Inside these two tags, you add the content. Look at the result:
{% codepen https://codepen.io/franca_/pen/BaorrdO default-tab=html,result %}

Here's a flock of sheep. The sheep is our content. They graze inside a fence, which has an entry and an exit. You always need both: _entry_ and _exit_.

![h1 opening and closing tag](https://dev-to-uploads.s3.amazonaws.com/i/on0ddidwv1fhxr5225nx.png)

Tags are not _visible_ on websites but they are **all over the place**. Everything you read is put into tags that get interpreted by the browser. 

_Silent instructions to the browser how to display our websites._


But, as said before, secret writing. There are many tags: paragraphs, quotes, line breaks and so much more. The browser obediently reads them all. 

A heading with a paragraph would look like this:

```html
<h1>My glorious heading ✨</h1>
<p>I don't know what I'm doing here</p>
```

Here's a new tag, the `<p>`, which stands for _paragraph_. We use it all the time.

In my previous article, we learned about HTML meaning _HyperText Markup Language_. Every language that consists of tags is called _Markup Language_. HTML is not the only one, for example in React you need XML.

## Now it's your turn! 💪🏽

You can practice below, simply add something! ↓
Click "Edit on Codepen" in the top right corner. You don't need an account to edit.

{% codepen https://codepen.io/franca_/pen/BaorJMj default-tab=html,result %}

---


## Interesting links about this topic

An introduction to markup languages
https://www.lifewire.com/what-are-markup-languages-3468655

Who is Tim?
https://www.britannica.com/biography/Tim-Berners-Lee

HTML intro at Mozilla Web Docs
https://developer.mozilla.org/en-US/docs/Web/HTML
