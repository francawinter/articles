# React children 👶 💬

React is great for building reusable components. Components often come in multiple variations – most of the time we can pass **props** to the component and all good.
```js
<Button color="red" text="Click me!" />
```

However, what if we build a component that doesn’t only change in style but also contains different JSX? This is often the case with interactive components like accordions, carousels and tabs or very big components.

Image a `Post` component for a blog post. All posts look alike, but vary in content.

![alt text](./assets/react-children-01.png)

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
*Note: the empty `<>` tag is a [Fragment](https://reactjs.org/docs/fragments.html#short-syntax).*

It’s just that this solution doesn’t look simple and clean. It’s not that we want to pass certain properties to the component, it’s more that we want to **definde what’s inside**.  In this case, use React children!

You don’t pass children like a property, you place it **inside the component tags** as if you'd write plain old HTML.

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

![alt text](./assets/react-children-02.png)

But – we have to tweak the component itself a little. At the moment, the Post component looks like this:
```js
// Post.js
export const Post = () => { ... }
```

As children are special properties, you don’t have to declare them when using the component, but you have to tell the component itself that children are welcome. The word `children` is a special word in the React world with a set meaning like `function` or `const`.

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

![alt text](./assets/react-children-03.png)

## ⚠️ Caution
Only use children if you can’t control the component’s content. If you know that a component is always going to be based on the same JSX structure, it’s better to pass string props for the heading, etc. **Be as strict as possible.**

Also, don’t try to style the children. Don’t do this:
```js
// App.js
<Post>
  <h1 className="post__heading">My first Post</h1>
  <p>Some intro text</p>
  <p>A paragaph</p>
</Post>
```
You don’t have a place to define that CSS class. 

There are several options in this case:

### 1. Create smaller components

If the heading is used universally, you could create a Heading component:

```js
// App.js
<Post>
  <Heading>My first Post</Heading>
  <p>Some intro text</p>
  <p>A paragaph</p>
</Post>
```

### 2. Use props instead

If you want to use a special `post__heading` class, the component itself is the right place to do this. Just pass the heading as a normal prop.
```js
// App.js
<Post heading="My first Post">
  <p>Some intro text</p>
  <p>A paragaph</p>
</Post>
```

```js
// Post.js
export const Post = ({ heading, children }) => {
  return (
    <section>
      <div className="post">
        <h1 className="post__heading">{heading}</h1>
        {children}
      </div>
      <a>See all posts</a>
    </section>
  );
};
```

### 3. Split component into smaller functions

This is my advice if you want to style the children specifically and use more than one JSX tag.
```js
// App.js
<Post heading="My first Post">
  <p>Some intro text</p>
  <p>A paragaph</p>
</Post>
```

```js
// Post.js
const PostMain = ({ content }) => {
  return <div className="post__main">{content}</div>;
};

export const Post = ({ heading, children }) => {
  return (
    <section>
      <div className="post">
        <h1 className="post__heading">{heading}</h1>
        <PostMain content={children} />
      </div>
      <a>See all posts</a>
    </section>
  );
};
```

## Advanced case: Split up your children

We can go even further and split our `Post` components in intro, main and outro.
//TODO: make it happen :)

---

## Linklist
- [React Fragments](https://reactjs.org/docs/fragments.html#short-syntax)
