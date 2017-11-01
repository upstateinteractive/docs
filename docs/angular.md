# And Angular was Good.

## Intro
Angular is Angular 2+. And 2+2 is 4. So after Angular 2 comes Angular 4.  
  
We use Angular as our front-end framework of choice. It's a full-featured framework that uses modern patterns such as Composable Components and One-Way Data Flows.  
  
There is a lot of information out there. Some good. Some bad. But here you'll find our standards on what is right. 

## Table of Contents
1. [Installing Angular CLI](#installing-angular-cli)
2. [Starting A New Project](#starting-a-new-project)  
3. [Routing](#routing)
4. [Webpack Bundle Analyzer](#webpack-bundle-analyzer)

### Installing Angular CLI
> We use [Angular CLI](https://cli.angular.io) on all of our new projects. The CLI starts the project with sensible defaults and makes it simple to generate new components, modules, etc...  
  

**Before you install angular cli,** you'll need [npm](https://docs.npmjs.com/getting-started/installing-node) and [yarn](https://yarnpkg.com/en/docs/install).  

_Install Angular CLI_
```bash
npm install -g @angular/cli
```

_Set Yarn as default package manager_
```bash
ng set --global packageManager=yarn  
```

### Starting A New Project

```bash 
ng new PROJECT-NAME
cd PROJECT-NAME
ng serve
```

#### Generating Common Files
```bash 
ng g component my-new-component
ng g service my-new-service
ng g module my-new-module
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

### Routing
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