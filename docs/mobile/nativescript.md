# And NativeScript was Good.

## Intro
NativeScript is an opensource framework to develop apps on the iOS and Android platforms. NativeScript can be built with JavaScript or any language that transpiles down to JavaScript. 

We use NativeScript with Angular as our front-end framework of choice for native, cross-platform mobile or mobile & web applications. 

Why NativeScript? It is a cost-effective way to build truly native cross-platform mobile apps. Companies can hire web developers to build cross-platform apps (iOS, Android, Web) in one codebase, rather than hiring a web developer, Java developer and Swift developer to build three separate apps. NativeScript uses the iOS and Android SDKs to access mobile device hardware, which makes it competitive on performance. Comparable frameworks to NativeScript include React Native and Flutter.
![shared project](../files/app-graphic.png)

## Table of Contents
1. [Codesharing with NativeScript](#codesharing-with-nativescript)
2. [Starting a New Shared Project](#starting-a-new-shared-project) 
3. [Structure of a Shared Project](#structure-of-a-shared-project) 
4. [HTTP with a Shared Project](#http-with-a-shared-project)
5. [Building and Running in Development](#building-and-running-in-development)

### Codesharing with NativeScript
------
> There are two options for codesharing with NativeScript. [xplat by nstudio](https://nstudio.io/xplat/) or [NativeScript Schematics](https://github.com/NativeScript/nativescript-schematics). We prefer the NativeScript Schematics approach with our cross-platform projects because it maintains the structure of an Angular app while generating components that can work across platforms.

* xplat is an open source value pack for Nx in order to provide out of the box support for cross-platform mobile development. You should have some familiarity with Nx to work with xplat. It has an opinionated structure and schematics built on top of the Angular CLI.
* NativeScript schematics uses the Angular CLI to generate components in NativeScript Angular apps. It now supports code sharing (web & mobile) to support NativeScript only, NativeScript & Web, and migrating to shared apps.

### Starting a New Shared Project
------

**You should be using @angular/cli@6.1.0 or newer and NativeScript CLI 5 or newer.**  

#### 1. Updates
- Angular CLI 
```bash
npm i -g @angular/cli
```

- NativeScript CLI 
```bash
npm install -g nativescript
```

- NativeScript application, platforms, webpack, typescript etc. (if applicable) by following the release [notes](https://docs.nativescript.org/releases/upgrade-instructions)


#### 2. Install NativeScript Schematics
```bash
npm i -g @nativescript/schematics
```

#### 3. Generate a new project with Schematics 

The NS Schematics [docs](https://github.com/NativeScript/nativescript-schematics) outline specific schematics and flags to generate a new app for just mobile or shared mobile + web. The basic commands are below:

Shared (Web & Mobile)
```bash
ng new --collection=@nativescript/schematics my-shared-app --shared
```

NativeScript Only
```bash
npm i -g @nativescript/schematics
```

#### 4. Generate Components, Modules, Directives

With Schematics set up, you can easily generate any angular building unit by using the Angular CLI "generate" command.
```bash
ng g c component-name
```

#### 5. Install [ngrx](https://ngrx.io/)
```bash
npm i -S @ngrx/store @ngrx/store-devtools @ngrx/entity @ngrx/effects
```

### Structure of a Shared Project
------
The objective is to share as much code as possible, and split the platform-specific code into separate files.

![shared project](../files/ns_codesharing.png)

This usually means that we can share the code for:

- Routes for navigation
- Services for common business logic 
- Component Class definition for common behaviour of a component 

while, splitting the code for:

- UI Layer (CSS and HTML) - as you need to use different user interface components in web and NativeScript-built native apps,
- NgModules - so that you can import platform-specific modules, without creating conflicts (e.g. Angular Material Design - which is web only) between web and mobile.

To create a platform specific file just requires a naming convention. For example, to create two separate html templates in your component, you would create `filename.component.html` for web and `filename.component.tns.html` for NativeScript. You can further specify the NativeScript files as specifically ios or android with an additional naming convention.

- [Code Splitting](https://docs.nativescript.org/angular/code-sharing/code-splitting)
- [Platform Specific Components](https://docs.nativescript.org/angular/code-sharing/platform-specific-components)

### HTTP with a Shared Project
------
For dependencies that are specific to web or mobile, you will need to import them into modules separately. In your new project, you'll notice two root modules `app.module.ts` for web and `app.module.tns.ts` for mobile. 

#### Web:
- import the following into the `app.module.ts`
```bash
import { HttpClientModule } from '@angular/common/http' 

@NgModule({
  imports: [
    HttpClientModule
  ]
})
export class MyModule { }
```

#### Mobile:
- import the following into the `app.module.tns.ts`
```bash
import { NativeScriptHttpClientModule } from 'nativescript-angular/http-client';

@NgModule({
  imports: [
    NativeScriptHttpClientModule
  ]
})
export class MyModule { }
```

#### Shared:
- Import the following into the shared ApiService. Dependency injection will detect which http module to use for each platform.
```bash
import { HttpClient, HttpHeaders } from '@angular/common/http';
```

Example `services/api.service.ts`
```bash
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { environment } from '../../environments/environment';

@Injectable({
  providedIn: 'root'
})
export class ApiService {

  private apiURL = environment.apiUrl;

  constructor(private http: HttpClient) { }

  getAll() {
    return this.http.get(`${this.apiURL}/category`, {
    });
  }

}
```

### Building and Running in Development
------

#### Setting up Xcode
1. In Xcode, add your Apple Id to your Xcode account
  - `Preferences > Account`  (add your Apple ID)
2. Add your developer certificate to your Apple ID
  - `Preferences > Account > Manage certificates > + iOS Development`

#### Run App on Emulator or Device from terminal:
1. [NativeScript documentation](https://docs.nativescript.org/tooling/docs-cli/project/testing/run-ios) explains how to run your project to a connected iOS device or iOS simulator from the terminal
  - `tns run ios --bundle`

#### Run App on Simulator or Device from XCode
1. In the terminal, build your project for development
  - `tns build ios --bundle`
2. Open the project in xcode
  - In your newly built platforms folder open the Xcode workspace in Finder and double click to open the project in Xcode
3. Connect your iOS device
  - If you're automatically generating the distribution provisional profile in xode, xcode will automatically add your device while it's connected. If you do it manually, you have to add your device udid code to the Apple Developer account.
  - In the general section of the project update the identity and signing sections:
  - Make sure the Bundle ID matches what is in the Apple Developer Account
  - Add the correct team (Apple ID) and automatically manage signing
4. Run the app on your connected device or choose from the list of simulators

[Video](https://drive.google.com/file/d/10Ugve3Qy-2kCCHFIr9voknbu51bVONQQ/view?usp=sharing) showing the process of opening the workspace and running it on devices in XCode
