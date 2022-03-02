<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/React-icon.svg/1280px-React-icon.svg.png" width="200">

# Welcome to React!

This guide is intended to introduce you to [React](https://github.com/facebook/react), a performant, dynamic, and fun web development framework.

## Table of Contents

- [Intro: What is React?](#intro-what-is-react)
  - [JSX](#jsx)
- [Getting Started](#getting-started)
  - [Tooling](#tooling)
  - [TypeScript](#typescript)
  - [React Beyond Create React App](#react-beyond-create-react-app)
- [Your First Component](#your-first-component)
  - [Javascript in JSX](#javascript-in-jsx)
  - [Nested Components](#nested-components)
  - [Props](#props)
  - [Leveraging Arrays](#leveraging-arrays)
- [Hooks](#hooks)
  - [useState](#usestate)
    - [with TypeScript](#usestate-with-typescript)
  - [useEffect](#useeffect)
    - [with TypeScript](#useeffect-with-typescript)
  - [useReducer](#usereducer)
    - [with TypeScript](#usereducer-with-typescript)
  - [useContext](#usecontext)
    - [with TypeScript](#usecontext-with-typescript)
  - [useMemo](#usememo)
    - [with TypeScript](#usememo-with-typescript)
  - [useCallback](#usecallback)
    - [with TypeScript](#usecallback-with-typescript)
- [Routing](#routing)
  - [Installation && Setup](#installation--setup)
  - [React Router v6](#react-router-v6)
- [Resources](#resources)

## Intro: What is React?

React is a front-end framework that combines HTML, CSS, and JS into JSX. It uses a component-based structure to create dynamic and performant web applications. In addition, its syntax known as **JSX** allows for inline addition of JavaScript to HTML.

#### JSX

Take a look at the following code snippet:

```html
<button id="primary-click"></button>
```

```js
const primaryButton = button.querySelector("#primary-click");
primaryButton.onclick = () => console.log("Primary!");
```

Now the same code expressed with JSX:

```html
<button
  className="primary"
  id="primary-click"
  onClick={() => console.log("Primary!")}
/>
```

JSX uses camelCase on all attributes, and curly braces for all non-string attribute values (numbers, booleans, functions).

## Getting Started

To get started on your React journey, you'll need a machine with [Node.js](https://nodejs.org/en/), preferably above v12. You can use [NVM](https://github.com/nvm-sh/nvm) to install and manage your Node version if it's not already installed.

### Tooling

When starting a new React project, most developers will reach for [Create-React-App](https://create-react-app.dev/), the default React app generator. To generate a new React application, we can run the following command in the terminal:

```sh
# with npm
npx create-react-app name-of-app
# or with yarn
yarn create react-app name-of-app
```

This will, most notably, install **react** (responsible for JSX), **react-dom** (responsible for rendering to the DOM), and **react-scripts** (responsible for tasks like builds and dev servers ).

It will also generate a new application with the following folder structure (as of v17.0.2):

```
name-of-app
├── README.md
├── node_modules
│   ├── ...
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   ├── reportWebVitals.js
│   └── setupTests.js
└── yarn.lock
```

To start the application, you can run the following in the terminal:

```sh
# with npm
npm start
# or with yarn
yarn start
```

### TypeScript

If you would like to use React with TypeScript, you can either [convert an existing project to TypeScript](https://www.typescriptlang.org/docs/handbook/migrating-from-javascript.html) or you can initialize a new React + TypeScript application with Create React App:

```sh
# with npm
npx create-react-app name-of-app --template typescript
# or with yarn
yarn create react-app my-app --template typescript
```

The app will generate with the following structure:

```
name-of-app
├── README.md
├── node_modules
│   ├── ...
├── package.json
├── public
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src
│   ├── App.css
│   ├── App.test.tsx
│   ├── App.tsx
│   ├── index.css
│   ├── index.tsx
│   ├── logo.svg
│   ├── react-app-env.d.ts
│   ├── reportWebVitals.ts
│   └── setupTests.ts
├── tsconfig.json
└── yarn.lock
```

### React Beyond Create React App

React is also used in a number of other popular front-end frameworks such as [Next.js](https://nextjs.org/) and [Gatsby.js](https://www.gatsbyjs.com/), as well as in native frameworks like [React Native](https://reactnative.dev/).

## Your First Component

A React **component** is (most commonly) a function that returns **JSX** or `null`.

Within your newly created application, open `src/App.js` and replace the content with the following:

```jsx
// src/App.js
function App() {
  return <h1>Hello World!</h1>;
}

export default App;
```

Start your application by running either `npm start` or `yarn start` in the same folder as your `package.json`.

Within the newly opened browser window (at `http://localhost:3000`), you should see a heading with "Hello World!" on the page. Your React app will render to the page via the div with an id of `#root`. Each component must render one top level element (i.e. you cannot have two adjacent tags at the top level).

> If you need to have adjacent tags without a container, you can use a `Fragment`, by adding empty opening and closing tags (`<> </>`) around the elements.

#### Javascript in JSX

If you want to use JavaScript within your JSX, add a set of curly braces around your expression!

```jsx
// src/App.js
function App() {
  const name = "your name here";
  return <h1>Hello World, I'm {name}!</h1>;
}

export default App;
```

### Nested Components

Components can be rendered within one another, by importing them and using angle brackets (e.g. `<Header></Header>` or `<Header/>`). Let's create a new component in `src/Post.jsx` and import it into `src/App.js`!

```jsx
// src/Post.jsx
const Post = () => {
  return (
    <article>
      <h3>Here's a header!</h3>
      <h4>This would be a good spot for an author.</h4>
      <p>And here's some body text. Consider this the content.</p>
    </article>
  );
};

export default Post;
```

```jsx
// src/App.js
import Post from "./Post";

function App() {
  const name = "your name here";
  return (
    <main>
      <h1>Hello World, I'm {name}!</h1>
      <Post />
    </main>
  );
}

export default App;
```

You can use a component as many times as you want, as long as each actively rendered component has a unique `key`:

```jsx
// src/App.js
import Post from "./Post";

function App() {
  const name = "your name here";
  return (
    <main>
      <h1>Hello World, I'm {name}!</h1>
      <Post key={0} />
      <Post key={1} />
    </main>
  );
}

export default App;
```

If you add an attribute to a component like above, it's called a prop! `props` can be used to pass down information from component to component.

> `key` is an exception to this rule, as it is not accessible in the child component.

### Props

`props` allow us to use attribute syntax to pass down information from component to component. All `props` apart from strings using single or double quotes should be enclosed in curly brackets. To pass props to a component, we must also add `props` as the child component's first argument.

Let's make our `Post` a bit more dynamic by adding some `props`!

```jsx
// src/App.js
import Post from "./Post";

function App() {
  const name = "your name here";
  return (
    <main>
      <h1>Hello World, I'm {name}!</h1>
      <Post
        key={0}
        author={name}
        body={"Writing blog posts is really fun!"}
        title="My First Blog Post"
      />
      <Post key={1} />
    </main>
  );
}

export default App;
```

```jsx
// src/Post.jsx
const Post = (props) => {
  return (
    <article>
      <h3>{props.title}</h3>
      <h4>{props.author}</h4>
      <p>{props.body}</p>
    </article>
  );
};

export default Post;
```

Now one of our `Post` components is displaying text, and the other does not. Try passing the second `Post` some example `author`, `body`, and `title` props.

### Leveraging Arrays

Unless you have a fixed number of items to render, it can often be more practical to use an array of an objects and the `.map` function to render components. Let's take our existing example and change it to use `.map`, as well as a single prop for all of the post's information:

```jsx
// src/App.js
import Post from "./Post";

function App() {
  const name = "your name here";
  // this array could also be imported in
  const blogPosts = [
    { 
      author: name,
      body: "Writing blog posts is really fun!",
      title: "My First Blog Post"
    },
    { 
      author: "Some Other Author",
      body: "Here is a second post to provide an example.",
      title: "My Second Blog Post"
    }
  ]
  return (
    <main>
      <h1>Hello World, I'm {name}!</h1>
      {posts.map((post, index) => (
        <Post key={index} post={post} />
      ))}
    </main>
  );
}

export default App;
```

```jsx
// src/Post.jsx
const Post = (props) => {
  return (
    <article>
      <h3>{props.post.title}</h3>
      <h4>{props.post.author}</h4>
      <p>{props.post.body}</p>
    </article>
  );
};

export default Post;
```

If any new items are added to the `blogPosts` array, a new `Post` will be rendered and passed the post's information as `props`. However, the array is currently static, as it's being redeclared on each render.

This brings up the following questions:

1. When does a component re-render?
2. How can we change data in a persistent way within a React application?
3. How can we avoid recomputing information declared within a component?
4. How can we share information between components outside of props?
5. How can we run side effects after or between re-renders?

For most, if not all of these questions, the answer lies in different React **hooks**.

1. a component re-renders whenever its `props` or **state** change. **State** in a React application is a unique type of variable that preserves data between re-renders. It can be created using the `useState` and `useReducer` hooks.
2. to change data and have it persist, you can update a component's state. All child components using that state will be re-rendered to show the new information.
3. both `useMemo` and `useCallback` serve to avoid re-computing values or functions respectively.
4. to share information without props, you can implement `useContext` to selectively bring in any information stored within that particular context.
5. to run side effects depending on state/props updates, you can add a `useEffect` that runs whenever stateful variables or props change.

Let's go ahead and try implementing these hooks!

## Hooks

### useState

#### useState with TypeScript

### useEffect

#### useEffect with TypeScript

### useReducer

#### useReducer with TypeScript

### useContext

#### useContext with TypeScript

### useMemo

#### useMemo with TypeScript

### useCallback

#### useCallback with TypeScript

## State Management

Considering all the above types of creating and distributing state across an application, there are also many ways of managing said state outside of React. [Redux](https://redux.js.org/) and its companion [Redux Toolkit](https://redux-toolkit.js.org/) are the most commonly leveraged frameworks. You can read more on it in our document on it [here](./redux.md).

## Routing

### Installation && Setup

## Resources

## React Design Patterns
