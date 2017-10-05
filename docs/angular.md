# And Angular was Good.

## Intro
Angular is Angular 2+. And 2+2 is 4. So after Angular 2, comes Angular 4.  
  
We use Angular as our front-end framework of choice. It's a full-featured framework that uses modern patterns such as Composable Components and One-Way Data Flows.  
  
There is a lot of information out there. Some good. Some bad. But here you'll find our standards on what is right. 

## Table of Contents
1. [Installing Angular CLI](#installing-angular-cli)  
2. [Routing](#routing)

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

### Routing
> ```ng new project-name --routing```   
> The `--routing` flag will automatically add a new routing module to your project. Isn't that nice?

#### Fundamental Order of Routes
> The order of routes matters in Angular. The router directs to the first matching route. Therefore, the wildcard/page-not-found (`**`) route is last, always.

_Order of Routes_
```typescript 
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
