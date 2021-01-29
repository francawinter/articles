# React children 👶 💬

React is great for building reusable components. Components often come in multiple variations – most of the time we can pass **props** to the component and all good.
```js
<Button color="red" text="Click me!" />
```

However, what if we build a component that doesn’t only change in style but also contains different JSX? This is often the case with interactive components like accordions, carousels and tabs or very big components.

Image a `Post` component for a blog post. All posts look alike, but vary in content.

The Post component could look like this:

```js
// Post.js
export const Post = () => {
  return (
    <section>
      <div>...Post content here...</div>
      <a>See all posts</a>
    </section>
  );
};
```

It is *possible* to create a property that contains all kind of JSX like this:
```js
// App.js
<Post content={
  <>
    <h1>My first Post</h1>
    <p>Some intro text</p>
    <p>A paragaph</p>
  </>
}/>
```
*Note: the empty `<>` tag is a Fragment.*

It’s just that this solution doesn’t look simple and clean. It’s not that we want to pass certain properties to the component, it’s more that we want to **definde what’s inside**.  In this case, use React children!

You don’t pass children like a property, you place it **inside the component tags** as if you would write plain old HTML.

```js
// App.js
<Post>
  <h1>My first Post</h1>
  <p>Some intro text</p>
  <p>A paragaph</p>
</Post>
```
*This looks so much better!*

You created your own component `<Post>` and filled it with JSX tags. You can insert some of your own custom components as well!

But – we have to tweak the component itself a little. At the moment, the TabPanel component looks like this:
```js
// Post.js
export const Post = () => { ... }
```

As children are special properties, you don’t have to declare them when using the component, but you have to tell the component itself that children are welcome. The word "children" is a special word in the React world with a set meaning like "function" or "const".

```js
// Post.js
export const Post = ({children}) => { ... } 
```

In the next step, you have to define the children's location inside the component’s JSX structure:

```js
// Post.js
export const Post = ({ children }) => {
  return (
    <section>
      <div>{children}</div>
      <a>See all posts</a>
    </section>
  );
};
```

## ⚠️ Caution
Only use children if you can’t control the component’s content. If you know that a component always will based on the same JSX structure, it’s better to pass string props for the heading, etc. Be as strict as possible.

Also, don’t try to style the children. Don’t do this:
```js
// App.js
<TabPanel roundedCorners="true">
	<h1 class="tab-panel__heading">A Heading</h1>
	<p>Lot's of text</p>
  <p>Lot's of text</p>
</TabPanel>
```

You don’t have a place to define that CSS class. You several two options in this case. If the heading is used universally, you could create a Heading component:
1. Create smaller components
```js
// App.js
<TabPanel roundedCorners="true">
  <Heading>A heading</Heading>
	<p>Lot's of text</p>
	<p>Lot's of text</p>
</TabPanel>
```

2. If you want to use a special `tab-panel__heading` class, the component itself is the right place to do this. Just pass the heading as a normal prop.
```js
// App.js
<TabPanel roundedCorners="true" heading="A heading">
	<p>Lot's of text</p>
	<p>Lot's of text</p>
</TabPanel>
```

```js
// TabPanel.js
export const TabPanel = ({roundedCorners, children, heading}) => {
 return (
	<section>
		<h1>{heading}</h1>
		<div>{children}</div>
		<div>Other stuff</div>
  </section>
 )
}
```
