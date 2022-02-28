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

React is a front-end framework that combines HTML, CSS, and JS into JSX. It uses a component-based structure to create dynamic and performant web applications. In addition, its syntax known as __JSX__ allows for inline addition of JavaScript to HTML.

#### JSX

Take a look at the following code snippet:

```html
<button id="primary-click"></button>
```

```js
const primaryButton = button.querySelector('#primary-click')
primaryButton.onclick = () => console.log('Primary!')
```

Now the same code expressed with JSX:

```jsx
<button className="primary" id="primary-click" onClick={() => console.log('Primary!')} />
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

This will, most notably, install __react__ (responsible for JSX), __react-dom__ (responsible for rendering to the DOM), and __react-scripts__ (responsible for tasks like builds and dev servers ).

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

A React __component__ is (most commonly) a function that returns __JSX__ or `null`.

Within your newly created application, open `src/App.js` and replace the content with the following:

```jsx
// src/App.js
function App() {
  return (
    <h1>Hello World!</h1>
  )
}

export default App;
```

Start your application by running either `npm start` or `yarn start` in the same folder as your `package.json`.

Within the newly opened browser window (at `http://localhost:3000`), you should see a heading with "Hello World!" on the page. Your React app will render to the page via the div with an id of `#root`.
## Props


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

