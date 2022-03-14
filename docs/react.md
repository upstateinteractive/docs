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
  - [A Note on the Virtual DOM](#a-note-on-the-virtual-dom)
  - [Javascript in JSX](#javascript-in-jsx)
  - [Nested Components](#nested-components)
  - [Props](#props)
    - [Other Reserved Words In Props And Attributes](#other-reserved-words-in-props-and-attributes)
  - [Leveraging Arrays](#leveraging-arrays)
- [Hooks](#hooks)
  - [useState](#usestate)
    - [with TypeScript](#usestate-with-typescript)
  - [useEffect](#useeffect)
    - [The Component Lifecycle](#the-component-lifecycle)
    - [Effects vs. Cleanup](#effects-vs-cleanup)
  - [useMemo](#usememo)
  - [useContext](#usecontext)
    - [with TypeScript](#usecontext-with-typescript) 
- [Tooling Beyond React](#tooling-beyond-react)
  - [State Management (Redux)](#state-management-redux)
  - [Routing (React Router)](#routing-react-router)
  - [Design Systems (Storybook)](#design-systems-storybook)
- [Additional Resources](#additional-resources)

## Intro: What is React?

React is a front-end framework that combines HTML, CSS, and JS into JSX. It uses a **component**-based structure to create dynamic and performant web applications. In addition, its syntax known as **JSX** allows for inline addition of JavaScript to HTML. It uses a **Virtual DOM** to simulate events and reduce re-rendering of elements.

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

```jsx
<button className="primary" id="primary-click" onClick={() => console.log("Primary!")} />
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

### A Note on the Virtual DOM

Now that we've created a component, how is it rendered to the `div#root`? In a React app created by `create-react-app` we can look within `src/index.js`, where the `ReactDOM.render` method takes a component / component tree to render, and creates an entry point within the element it is passed (known as the React root).

```jsx
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import reportWebVitals from "./reportWebVitals";

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);

reportWebVitals();
```

In this case, the application is being rendered within the `div#root` present within the `public/index.html` file.

### Javascript in JSX

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

#### Other Reserved Words in Props and Attributes

Similar to `key`, there are other reserved words that have either have specific functions as props or JSX attributes.

##### ref

`ref` is used by React to target for events within components, and is not passed down as a prop to the child component.

##### style

In vanilla HTML, it's possible to pass a string of CSS style properties to an element to style it inline. In React, instead of passing a string, you can pass an object of CSS style properties in camelCase:

```jsx
// src/Post.jsx
const Post = (props) => {
  const postStyles = {
    display: "flex",
    flexDirection: "column",
    alignItems: "center",
    justifyContent: "center",
  };

  return (
    <article style={postStyles} className="post">
      <h3>{props.title}</h3>
      <h4>{props.author}</h4>
      <p>{props.body}</p>
    </article>
  );
};

export default Post;
```

##### className

When working with JSX elements, the `class` keyword is reserved, so all instances should be replaced with `className`:

```jsx
// src/Post.jsx
const Post = (props) => {
  return (
    <article className="post">
      <h3>{props.title}</h3>
      <h4>{props.author}</h4>
      <p>{props.body}</p>
    </article>
  );
};

export default Post;
```

##### children

Components can be rendered as self-closing tags or open and closing tags. If rendered with opening and closing tags, the `children` prop can be used to render any elements or components within the two tags:

```jsx
const Container = (props) => {
  return <main>{props.children}</main>;
};

const Page = () => {
  return (
    <Container>
      <h1>Welcome to Our Page!</h1>
      <article>
        <h3>How To Make a React Component</h3>
        <p>You got this!</p>
      </article>
    </Container>
  );
};

export default Page;
```

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
      title: "My First Blog Post",
    },
    {
      author: "Some Other Author",
      body: "Here is a second post to provide an example.",
      title: "My Second Blog Post",
    },
  ];
  return (
    <main>
      <h1>Hello World, I'm {name}!</h1>
      {blogPosts.map((post, index) => (
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
    <article className="post">
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

For most, if not all of these questions, the answer lies in different React **hooks**:

1. a component re-renders whenever its `props` or **state** change. **State** in a React application is a unique type of variable that preserves data between re-renders. It can be created using the `useState` and `useReducer` hooks.
2. to change data and have it persist, you can update a component's state. All child components using that state (via props or context) will be re-rendered to show the new information.
3. both `useMemo` and `useCallback` serve to avoid re-computing values or functions respectively.
4. to share information without props, you can implement `useContext` to selectively bring in any information stored within that particular context.
5. to run side effects depending on state/props updates, you can add a `useEffect` that runs whenever stateful variables or props change.

Let's go ahead and try implementing these hooks!

## Hooks

This section introduces a series of hooks provided by React that provide essential storage and lifecycle functionality. When working in React, most information is redeclared upon each render—the general exception to this rule are imports and React hooks. We can recognize a React hook because it will always start with `use` Hooks should not be called conditionally, in the same order, and before any other functions declared in the component. Let's see how they can be used to make changes to persistent data.

### useState

The `useState` hook can be used to create persistent, mutable data. Declaring a `useState` yields a state getter, and a state setter.

```js
const [getter, setter] = useState(initialValue);
```

```jsx
import { useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <span>This is the current count: {count}</span>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
};

export default Counter;
```

Let's return to our example from before and apply state with the `useState` hook.

```jsx
// src/Post.jsx
import { useState } from "react";

const Post = (props) => {
  const [like, setLike] = useState(false);

  return (
    <article className="post">
      <h3>{props.post.title}</h3>
      <h4>{props.post.author}</h4>
      <p>{props.post.body}</p>
      {/* event handlers can be attached with attributes (e.g. onEventNameInCamelCase) */}
      <button onClick={() => setLike(!like)}>{like ? "★" : "☆"}</button>
    </article>
  );
};

export default Post;
```

#### useState with TypeScript

Implementing `useState` with TypeScript only requires declaring a type on the hook itself.

```tsx
// src/Post.tsx
import { useState } from "react";

// make sure to add a type definition for your props
interface Props {
  post: { title: string; author: string; body: string };
}

const Post = (props: Props) => {
  // useState can take a type argument
  const [like, setLike] = useState<boolean>(false);

  return (
    <article className="post">
      <h3>{props.post.title}</h3>
      <h4>{props.post.author}</h4>
      <p>{props.post.body}</p>
      <button onClick={() => setLike(!like)}>{like ? "★" : "☆"}</button>
    </article>
  );
};

export default Post;
```

### useEffect

The `useEffect` hook is used to run side effects upon component mounting, state and props updates, and component unmounting.

A `useEffect` typically looks like this:

```js
useEffect(() => {
  console.log("do something");
  setSomeOtherState(someState);
}, [someState, someProps, someOtherProps]);
```

The first argument is the code that runs between updates, also known as the effect. The second (and optional) argument is the dependency array—if any of the variables within the array are updated, the effect runs. If no variables are present, but the array is present, the effect runs once only on mount. If there is no second argument, the effect runs upon each re-render.

#### The Component Lifecycle

The **component lifecycle** refers to the events that occur during a component's rendering, its state and props updates, and its eventual unrendering.

When a component first renders to the screen successfully, it's referred to as **mounting**. After this initial render, the component will re-render depending on `state` and `props` updates, and finally **unmount** when the component is no longer rendered on the screen.

```jsx
// src/Post.jsx
import { useEffect, useState } from "react";

const Post = (props) => {
  const [like, setLike] = useState(false);

  useEffect(() => {
    console.log("The like variable has changed!");
  }, [like]);

  useEffect(() => {
    console.log("The component has mounted!");
  }, []);

  useEffect(() => {
    console.log("The component has re-rendered!");
  });

  return (
    <article className="post">
      <h3>{props.post.title}</h3>
      <h4>{props.post.author}</h4>
      <p>{props.post.body}</p>
      {/* event handlers can be attached with attributes (e.g. onEventNameInCamelCase) */}
      <button onClick={() => setLike(!like)}>{like ? "★" : "☆"}</button>
    </article>
  );
};

export default Post;
```

#### Effects vs. Cleanup

In addition to a side effect, a **cleanup** function can be used to run items between renders. To use it, return a function from within the `useEffect`:

```jsx
import { useEffect, useState } from "react";

const Counter = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count has been updated!");
    return () => {
      console.log("Count is about to be updated!");
    };
  }, [count]);

  return (
    <div>
      <span>This is the current count: {count}</span>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
};

export default Counter;
```

To keep track of when effects and cleanups run with different dependency arrays, you can refer to this chart:

|         Dependency Array          |             Effect              |          Cleanup           |
| :-------------------------------: | :-----------------------------: | :------------------------: |
|            Empty: (``)            |       Runs every render.        | Runs before every render.  |
|        Empty array: (`[]`)        |    Runs on component mount.     | Runs on component unmount. |
| Array: (`[someState, someProps]`) | Runs whenever variables update. |   Runs between updates.    |

### useMemo

The `useMemo` hook can be used to reduce recomputation of values declared within components.

A `useMemo` will usually look like this:

```js
const memoizedValue = useMemo(
  () => expensiveComputation(someArg, someOtherArg),
  [someArg, someOtherArg]
);
```

Similar to a useEffect, `useMemo` takes two arguments: the function/value to be computed and an array of values, that when changed, will cause the `useMemo` to recompute the values.

Consider the following example, using our `Post` component from earlier:

```jsx
import Post from "./Post";

const Forum = (props) => {
  const [comment, setComment] = useState("");
  // recomputes every render
  const postsByAuthor = props.posts.sort((a, b) => a.author - b.author);

  return (
    <main>
      <form>
        <input
          type="text"
          value={comment}
          onChange={(e) => setComment(e.target.value)}
        />
      </form>
      <section>
        <h3>Unmemoized Posts</h3>
        {postsByAuthor.map((post) => (
          <Post post={post} />
        ))}
      </section>
    </main>
  );
};

export default Forum;
```

The above example will re-render each time that `comment` is updated. Let's add `useMemo` to only recompute the sorted posts when they are updated:

```jsx
import { useMemo } from "react";
import Post from "./Post";

const Forum = (props) => {
  const [comment, setComment] = useState("");
  // recomputes only when posts change
  const memoizedPostsByAuthor = useMemo(
    props.posts.sort((a, b) => a.author - b.author),
    [props.posts]
  );

  return (
    <main>
      <form>
        <input
          type="text"
          value={comment}
          onChange={(e) => setComment(e.target.value)}
        />
      </form>
      <section>
        <h3>Memoized Posts</h3>
        {memoizedPostsByAuthor.map((post) => (
          <Post post={post} />
        ))}
      </section>
    </main>
  );
};

export default Forum;
```

### useContext

The `useContext` hook can be used to pass information around an application without the use of props.

Setting up a `useContext` requires a bit more setup, as there are two parts: the `context` and the `provider`. The `context` is a reference to the information, and the `provider` is a component wrapper which provides the information referenced. To access the context, use the `useContext` hook with the

Setting up a `useContext` usually looks like this:

```jsx
// src/context/index.js
import { createContext, useContext } from "react";

export const AppContext = createContext({});
// use the displayName property to update the context's name within the Components tab
AppContext.displayName = "AppContext";
export const useAppContext = () => useContext(AppContext);

export const AppContextProvider = ({ children }) => {
  const value = {};

  return <AppContext.Provider value={value}>{children}</AppContext.Provider>;
};

export default AppContextProvider;
```

Within the context's provider, you can also implement other React hooks, such as `useEffect` and `useState`:

```jsx
// src/context/index.js
import { createContext, useContext, useEffect, useState } from "react";

export const AppContext = createContext({});
AppContext.displayName = "AppContext";
export const useAppContext = () => useContext(AppContext);

export const AppContextProvider = ({ children }) => {
  const [records, setRecords] = useState([]);

  useEffect(() => {
    fetch("/api/records")
      .then((res) => res.json())
      .then((data) => setRecords(data))
      .catch((e) => console.error(e));
  }, []);

  const value = {
    records,
    setRecords,
  };

  return <AppContext.Provider value={value}>{children}</AppContext.Provider>;
};

export default AppContextProvider;
```

This context can then be added around any component (or around the `App` component) to allow access or updates to this information for child components:

```jsx
// src/index.js

import React from "react";
import ReactDOM from "react-dom";
import "./index.css";
import App from "./App";
import { AppContextProvider } from "./context";
import reportWebVitals from "./reportWebVitals";

ReactDOM.render(
  <React.StrictMode>
    <AppContextProvider>
      <App />
    </AppContextProvider>
  </React.StrictMode>,
  document.getElementById("root")
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

```jsx
// src/App.js
import { useAppContext } from "./context";

function App() {
  // properties can be destructured from the context
  const { records } = useAppContext();

  return (
    <div className="App">
      {records.map((record) => (
        <p>{record.title}</p>
      ))}
    </div>
  );
}

export default App;
```

#### useContext with TypeScript

Using `useContext` with Typescript requires adding a type both to the `context` and the `provider`:

```tsx
// src/context/index.tsx
import {
  PropsWithChildren,
  createContext,
  useContext,
  useEffect,
  useState,
} from "react";

export type AppContextType = {
  records: string[];
  setRecords: (r: string[]) => void;
};
export const AppContext = createContext<AppContextType>({
  records: [],
  setRecords: () => {},
});
AppContext.displayName = "AppContext";
export const useAppContext = () => useContext(AppContext);

export const AppContextProvider = ({ children }: PropsWithChildren<{}>) => {
  const [records, setRecords] = useState<string[]>([]);

  useEffect(() => {
    fetch("/api/records")
      .then((res) => res.json())
      .then((data) => setRecords(data))
      .catch((e) => console.error(e));
  }, []);

  const value = {
    records,
    setRecords,
  };

  return <AppContext.Provider value={value}>{children}</AppContext.Provider>;
};

export default AppContextProvider;
```

## Tooling Beyond React

At this point, you can create a new React application and navigate through an existing codebase, so what comes next? The following sections detail additional features / frameworks to add to an application.

### State Management (Redux)

Considering all the above types of creating and distributing state across an application, there are also many ways of managing said state outside of React. [Redux](https://redux.js.org/) and its companion [Redux Toolkit](https://redux-toolkit.js.org/) are the most commonly leveraged frameworks. You can read more on it in our document on it [here](./redux.md).

### Routing (React Router)

While React is generally viewed as a single page application framework, routing can be implemented by using [React Router](https://www.npmjs.com/package/react-router-dom). React Router DOM has a few very different implementations, most notably `>=5.1 <6.0` and `>=6.0`. For developers approaching for the first time, make sure to read the [v6 documentation](https://reactrouter.com/docs/en/v6/getting-started/tutorial) If your upcoming project has `react-router-dom@<6`, then make sure to refer to the [v5.1 documentation](https://v5.reactrouter.com/web/guides/quick-start).

### Design Systems (Storybook)

[Storybook](https://storybook.js.org/) is a design system used to create dynamic UI components testable with "stories". It's often used in tandem with React to be able to test different variations on components.

## Additional Resources

- [React on GitHub](https://github.com/facebook/react)
- [React: Getting Started](https://reactjs.org/docs/getting-started.html)
