# Don’t interchange margin and padding

Spacing is one of the core elements of design. It’s something every designer learns early on: _Add whitespace. Elements need air to breathe._

As a consequence, I add CSS margins and paddings every day. It’s a magical feeling to see a button come to life with a little ~~margin~~  padding.

It’s one line of CSS that calms the eye immediately. 

![A button](https://dev-to-uploads.s3.amazonaws.com/i/i6f0xz4exa7ute33608p.jpg)

## Everything’s great, CSS is for babies anyway

For a long time, I didn’t really care too much about the differences between margin and padding. Nevertheless, I noticed these basic rules:

### padding

An element with a **background color** or **border** needs whitespace inside
	
 ![Padding example](https://dev-to-uploads.s3.amazonaws.com/i/i2t7sp5wia2iwzxvgqgy.jpg)

### margin

An element  needs air to breathe **outside** of its body
	
![Two elements with margin](https://dev-to-uploads.s3.amazonaws.com/i/j2a8dc0p8nsh881oqi0p.jpg)

I applied margins as external properties, padding for introspective. It made sense for me. But often, I couldn’t find a rule and randomly used one of them.

##  The point where I got confused

One of the cases I struggled with was headlines. Headlines and text often need a good amount of spacing between them.  `<h1>` comes with a default margin, which never seemed to help me in any way. 

```css
margin-top: 0.67em; margin-bottom: 0.67em; 🤔
```

![A h1 headline with default margin](https://dev-to-uploads.s3.amazonaws.com/i/p8jr8v7jize7fv774gaw.jpg)

Usually, I would remove this margin (which seemed arbitrarily to me) and applied my own `padding-bottom`, so it would fit the design perfectly. 

Satisfied with the outcome, I would go on. Eventually, when CMS content got in, I noticed a slightly larger spacing between headline and text. Dammit, these stupid default margins! All the paragraphs have them as well!

```css
margin-top: 1em; margin-bottom: 1em; 🤨
```

![h1 headline with padding bottom and paragraph below with default margin](https://dev-to-uploads.s3.amazonaws.com/i/vo5q0tnn8ux7jqypf76l.jpg)

What did I do? 
I wanted to maintain the spacing between two paragraphs, but not the first one. So I removed it with `p:first-of-type`. Now, the spacing would sit fine at least. Sigh.

![h1 headline with padding bottom and paragraph below without margin](https://dev-to-uploads.s3.amazonaws.com/i/o9suanzetzp13kwxvxwf.jpg)

This approach is against the natural behavior of CSS. There’s a reason these elements have default margins – and not paddings. **Don't fight it.**

## Use margins to your advantage!

The key understanding here is to _really_ let sink in what it means that margins can **collapse**. I read it a lot of times but I never saw the advantage over paddings. But in reality, margins are really powerful and clever! Margins can communicate with each other. They shine when combined. Paddings, on the contrary, are stubborn cats that never change. And sometimes, this is exactly the behavior we want.

This is extremely helpful when building a **design system** or generally using a **component-based approach**, e.g. React or Vue. 

Imagine a complete component, having padding top and bottom. Now, a second component gets stacked beneath it, containing padding as well. There will be a big gap between the two, too big.

![Two components with padding](https://dev-to-uploads.s3.amazonaws.com/i/0mnzhirofjblq97zs3q7.jpg)

If you use margins instead, **only the biggest margin will be applied**. 

![Two components with collapsing margins](https://dev-to-uploads.s3.amazonaws.com/i/d9wadpwfoqr37jlgprjw.jpg)

This is true for text layouts as well. Instead of using paddings on typography tags, use margins. If the default margin is too small, overwrite it with a bigger margin. The headings’ margin-bottom and the paragraph’s margin-top won’t add up anymore but instead, flow into each other nicely.

![A headline and paragraph with margin](https://dev-to-uploads.s3.amazonaws.com/i/9zeui4p1qbtxya3mc2s5.jpg)

Because HTML was invented for academic papers, it was useful to provide some tags with default styling. Even without any CSS, texts with semantic HTML is still readable. So don’t get angry with the default browser stylings, we have them for a reason! ♥️ 
