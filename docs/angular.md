# And Angular was Good.

## Intro
Angular is Angular 2+. And 2+2 is 4. So after Angular 2 comes Angular 4.  
  
We use Angular as our front-end framework of choice. It's a full-featured framework that uses modern patterns such as Composable Components and One-Way Data Flows.  
  
There is a lot of information out there. Some good. Some bad. But here you'll find our standards on what is right. 

## Table of Contents
1. [Installing Angular CLI](#installing-angular-cli)
2. [Starting A New Project](#starting-a-new-project)  
3. [Starting A New Universal Project](#starting-a-new-universal-project)
4. [Add TransferState](#add-transferstate)
5. [Routing](#routing)
6. [Webpack Bundle Analyzer](#webpack-bundle-analyzer)
7. [Using ngRx with a loading indicator](#using-ngrx-with-a-loading-indicator)

### Installing Angular CLI
------
> We use [Angular CLI](https://cli.angular.io) on all of our new projects. The CLI starts the project with sensible defaults and makes it simple to generate new components, modules, etc...  
  

**Before you install angular cli,** you'll need [npm](https://docs.npmjs.com/getting-started/installing-node) and [yarn](https://yarnpkg.com/en/docs/install).  

_Install Angular CLI_
```bash
npm install -g @angular/cli
```


### Starting A New Project
------
```bash 
ng new PROJECT-NAME --service-worker true --routing true --spec false --prefix COMPONENT-PREFIX
cd PROJECT-NAME
ng serve
```

#### Generating Common Files
```bash 
ng g component my-new-component
ng g service my-new-service
ng g module my-new-module
```

#### Common Installs
ngrx
```bash
npm i -S @ngrx/store @ngrx/store-devtools @ngrx/entity @ngrx/effects
npm i -D @ngrx/schematics
```
angular
```
npm i -S @angular-devkit/core @angular/material @angular/cdk
```

#### Adding Bootstrap
```bash
npm install bootstrap@4.0.0-alpha.6
```
> In your `angular-cli.json` file, add the following paths:

```bash
"styles": [
    "styles.css",
    "../node_modules/bootstrap/dist/css/bootstrap.min.css"
  ],
  "scripts": [
    "../node_modules/jquery/dist/jquery.min.js",
    "../node_modules/bootstrap/dist/js/bootstrap.min.js"
  ],
```

### Starting A New Universal Project
------
```bash 
ng new PROJECT-NAME --service-worker true --routing true --skipTests true --prefix COMPONENT-PREFIX

cd PROJECT-NAME

npm install --save @angular/platform-server @nguniversal/module-map-ngfactory-loader ts-loader express

ng generate universal PROJECT-NAME
```

#### Creating Node Server
Create a `server.ts` file in the root directory of the project and add the following code.
```ts
// These are important and needed before anything else
import 'zone.js/dist/zone-node';
import 'reflect-metadata';

import { renderModuleFactory } from '@angular/platform-server';
import { enableProdMode } from '@angular/core';

import * as express from 'express';
import { join } from 'path';
import { readFileSync } from 'fs';

// Faster server renders w/ Prod mode (dev mode never needed)
enableProdMode();

// Express server
const app = express();

const PORT = process.env.PORT || 4201;
const DIST_FOLDER = join(process.cwd(), 'dist');

// Our index.html we'll use as our template
const template = readFileSync(join(DIST_FOLDER, 'index.html')).toString();

// * NOTE :: leave this as require() since this file is built Dynamically from webpack
const { AppServerModuleNgFactory, LAZY_MODULE_MAP } = require('./dist-server/main.bundle');

const { provideModuleMap } = require('@nguniversal/module-map-ngfactory-loader');

app.engine('html', (_, options, callback) => {
  renderModuleFactory(AppServerModuleNgFactory, {
    // Our index.html
    document: template,
    url: options.req.url,
    // DI so that we can get lazy-loading to work differently (since we need it to just instantly render it)
    extraProviders: [
      provideModuleMap(LAZY_MODULE_MAP)
    ]
  }).then(html => {
    callback(null, html);
  });
});

app.set('view engine', 'html');
app.set('views', DIST_FOLDER);

// Server static files from dist folder
app.get('*.*', express.static(DIST_FOLDER));

// All regular routes use the Universal engine
app.get('*', (req, res) => {
  res.render('index', { req });
});

// Start up the Node server
app.listen(PORT, () => {
  console.log(`Node server listening on http://localhost:${PORT}`);
});
```

#### Creating webpack configuration
Create a `webpack.server.config.js` file in the root directory of the project and add the following code:

```ts
const path = require('path');
const webpack = require('webpack');
 
module.exports = {
    entry: { server: './server.ts' },
    resolve: { extensions: ['.ts', '.js'] },
    target: 'node',
    // this makes sure we include node_modules and other 3rd party libraries
    externals: [/(node_modules|main\..*\.js)/],
    output: {
        path: path.join(__dirname, 'dist'),
        filename: '[name].js'
    },
    module: {
        rules: [
            { test: /\.ts$/, loader: 'ts-loader' }
        ]
    },
    plugins: [
        // Temporary Fix for issue: https://github.com/angular/angular/issues/11580
        // for "WARNING Critical dependency: the request of a dependency is an expression"
        new webpack.ContextReplacementPlugin(
            /(.+)?angular(\\|\/)core(.+)?/,
            path.join(__dirname, 'src'), // location of your src
            {} // a map of your routes
        ),
        new webpack.ContextReplacementPlugin(
            /(.+)?express(\\|\/)(.+)?/,
            path.join(__dirname, 'src')
        )
    ]
};
```

#### Update package.json
```bash
"build-dev:ssr": "npm run dev:client-and-server-bundles && npm run webpack:server",
"dev:client-and-server-bundles": "ng build && ng build --prod --app 1 --output-hashing=false"
"build:ssr": "npm run build:client-and-server-bundles && npm run webpack:server",
"serve:ssr": "node dist/server.js",
"build:client-and-server-bundles": "ng build --prod && ng build --prod --app 1 --output-hashing=false",
"webpack:server": "webpack --config webpack.server.config.js --progress --colors"
```

#### Usage
To build in dev mode:
Run `npm run build-dev:ssr` to bundle your front-end assets 
Run `npm run serve:ssr` to serve your application on `localhost:4201`

To build in production mode:
Run `npm run build:ssr` to bundle your front-end assets 
Run `npm run serve:ssr` to serve your application on `localhost:4201`


### Add TransferState
------
Coming Soon


### Routing
------
> ```ng new project-name --routing```   
> The `--routing` flag will automatically add a new routing module to your project. Isn't that nice?

#### Fundamental Order of Routes
> The order of routes matters in Angular. The router directs to the first matching route. Therefore, the wildcard/page-not-found (`**`) route is last, always.

_Order of Routes_
```ts 
const appRoutes: Routes = [
  { 
    path: 'home', 
    component: HomeComponent 
  },
  { path: '',
    redirectTo: '/home',
    pathMatch: 'full'
  },
  { 
    path: '**', 
    component: PageNotFoundComponent 
  }
];
```


### Webpack Bundle Analyzer
------
> For when you want to keep your bundle small.


#### Setup
```bash
npm i -D webpack-bundle-analyzer serve
```

```json
// package.json
{
 "scripts": {
    "start": "./node_modules/.bin/serve dist/ --single",
    "bundle-report": "ng build --prod --build-optimizer --named-chunks --stats-json && ./node_modules/.bin/webpack-bundle-analyzer dist/stats.json"
  },
}
```

#### Usage
Run `npm run bundle-report` to generate a bundle report.

Run `npm start` to serve your optimized code and visit the network tab of your browser to determine the file size.

### Using ngRx with a loading indicator
------
Using ngrx with a loading indicator requires the following, by example from the [official example app search reducer](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts): 

1. [Add `loading` to your state](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts#L5)  
2. [Initialize to `false`](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts#L12)  
3. [In your SEARCH action, return state where `loading` is toggled to `true`](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts#L31-L37)  
4. [In your SEARCH_COMPLETE action return state where `loading` is toggled back to `false`](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts#L42)  
5. [Create a `getLoading function`](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/search.ts#L66)  
6. **Switch** to your `reducers/index.ts` file. [Create a selector for getLoading](https://github.com/ngrx/platform/blob/master/example-app/app/books/reducers/index.ts#L104-L107)  
7. In your component, [select `getLoading` from the store](https://github.com/ngrx/platform/blob/master/example-app/app/books/containers/find-book-page.ts#L27)  
8. [Use your store selection, in this case `searching$` on your component](https://github.com/ngrx/platform/blob/master/example-app/app/books/containers/find-book-page.ts#L14)  
9. [Use the value to toggle visibility of your loading indicator](https://github.com/ngrx/platform/blob/master/example-app/app/books/components/book-search.ts#L15)  

This general idea can be applied anywhere, replacing SEARCH with the action of the request (POST, GET, you get the point).   
  
It might be that you'll make subtle modifications to the above, but with these instructions you can make those decisions where necessary.  

Loading indicators are everywhere. So you can use this pattern across applications.  You can use it in native applications, web applications, and anywhere there is a screen and Angular. Not only can this pattern be used for loading indicators, you can use it for toggling the display of errors as well. 
  
Have fun! And make your loading indicator spin!
