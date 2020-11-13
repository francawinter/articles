# Don’t interchange margin and padding

Spacing is one of the core elements of design. It’s something every designer learns early on: _Add whitespace. Elements need air to breath._

As a consequence, I add CSS margins and paddings every day. It’s a magical feeling to see a button come to life with a little ~~margin~~  padding.

[picture with button]

It’s one line of CSS that calms the eye immediately. 


## Everything’s great, CSS is for babies anyway

For a long time, I didn’t really care too much about the differences between margin and padding. Nevertheless, I noticed these basic rules:

1. padding
	- An element with a ::background color:: or ::border:: needs whitespace inside
	
		[ Planet illustration 1 ]

2. margin
	- An element  needs air to breathe ::outside:: of its body
	
		[ Planet illustration 2 ]

I applied margins as external properties, padding for introspective. It made sense for me. But often, I couldn’t find a rule and randomly used one of them.


##  The point where I got confused

[ Some visual example ]

One of the cases I struggled with were headlines. Headlines and text often need a good amount of spacing between them.  `<h1>` comes with a default margin, which never seemed to help me in any way. 
```css
margin-top: 0.67em; margin-bottom: 0.67em; 🤔
```
Usually I would remove this margin (which seemed arbitrarily to me) and applied my own `padding-bottom`, so it would fit the design perfectly. 

Satisfied with the outcome, I would go on. Eventually, when CMS content got in, I noticed a slightly larger spacing between headline and text. Dammit, these stupid default margins! All the paragraphs have them as well!
```css
margin-top: 1em; margin-bottom: 1em; 🤨
```
What did I do? 
I wanted to maintain the spacing between two paragraphs, but not the first one. So I removed it with `p:first-of-type`. Now, the spacing would sit fine at least. Sigh.

This approach is against the natural behavior of CSS. There’s a reason these elements have default margins – and not paddings!


## Use margins to your advantage!
The key understanding here is to _really_ let sink in what it means that margins can **collapse**. I read it a lot of times but I never saw the advantage over paddings. But in reality, margins are really powerful and clever! Margins can communicate with each other. They shine when combined. Paddings, on the contrary, are stubborn cats that never change. And sometimes, this is exactly the behaviour we want.

This is extremely helpful when building a design system or generally using a component-based approach, e.g. React or Vue. 

Imagine a complete component, having padding top and bottom. Now, a second component gets stacked beneath it, containing padding as well. There will be a big gap between the two, too big.

[ Bild: 2 Komponenten mit zu großer Lücke ]

If you use margins instead, **only the biggest margin will be applied**. 

[ Bild: 2 Komponenten mit guter Lücke ]

This is true for text layouts as well. Instead of using paddings on typography tags, use margins. If the default margin is too small, overwrite it with a bigger margin. The headings’s margin-bottom and the paragraph’s margin-top won’t add up anymore, but instead flow into each other nicely.

Because HTML was invented for academic papers, it was useful to provide typographic tags with default styling. Even without any CSS, texts with semantic HTML is still readable. So don’t get angry with the default browser stylings, we have them for a reason! ♥️
