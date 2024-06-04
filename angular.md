# Angular 17 Documentation

## Introduction

Angular 17 is the latest version of the Angular framework. It offers improved performance, faster application builds, and a more efficient development experience [7](https://dev.to/sameerkatija/github-markdown-cheat-sheet-everything-you-need-to-know-to...) .

## Architecture Overview

Angular's architecture is composed of several key parts: modules, components, templates, services, and dependency injection. Below is a breakdown of these elements:

### Modules

Modules are containers for different parts of an application. At the root of every Angular application is the root module, typically called `AppModule`.

**File: `app.module.ts`**

- **Purpose:** Declares the root module and all imported modules that the application uses.
- **Content Example:**
``` ts
    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';
    import { AppComponent } from './app.component';
    import { MarkdownModule } from 'ngx-markdown';
    
    @NgModule({
      declarations: [AppComponent],
      imports: [BrowserModule, MarkdownModule.forRoot()],
      bootstrap: [AppComponent]
    })
    export class AppModule { }
    
    ```


### Components

Components are the basic building blocks of an Angular application. Each component has an HTML template, a CSS style, and a TypeScript class.

**File: `app.component.ts`**

- **Purpose:** Defines the root component of the application. It manages the view and logic of the app.
- **Content Example:**
    
    ```ts
    import { Component } from '@angular/core';
    
    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {
      title = 'angular-app';
    }
    ```
    

### Templates

Templates define the user interface of a component. They include HTML, data bindings, and Angular directives.

**File: `app.component.html`**

- **Purpose:** Contains HTML markup and Angular templating for the root component.
- **Content Example:**
    
    
    
    ```html
    <div>
      <h1>{{ title }}</h1>
      <markdown [data]="'# Hello, world!'"></markdown>
    </div>
    ```
    

### Services

Services provide business logic and data management. They can be injected into components or other services using Angular’s dependency injection system.

**File: `app.service.ts`**

- **Purpose:** Provides a reusable service for application-wide logic.
- **Content Example:**
    
    
    
    ```ts
    import { Injectable } from '@angular/core';
    
    @Injectable({
      providedIn: 'root'
    })
    export class AppService {
      getData() {
        return 'Service Data';
      }
    }
    ```
    

### Dependency Injection

Angular's dependency injection system allows components and services to declare dependencies they need, which are then injected by Angular.

**File: `app.component.ts` Updated**

- **Usage Example:**
    
    typescript
    
    ```ts
    import { Component } from '@angular/core';
    import { AppService } from './app.service';
    
    @Component({
      selector: 'app-root',
      templateUrl: './app.component.html',
      styleUrls: ['./app.component.css']
    })
    export class AppComponent {
      data: string;
    
      constructor(private appService: AppService) {
        this.data = this.appService.getData();
      }
    }
    ```
    

## Adding a Component

To add a new component:

1. Generate a new component using Angular CLI:
    
    
    
    ```sh
    ng generate component new-component
    ```
    
2. Angular CLI will create the following files:
    - `new-component/new-component.component.ts`
    - `new-component/new-component.component.html`
    - `new-component/new-component.component.css`

### Example Files Analysis

**File: `new-component.component.ts`**

- **Purpose:** Contains the logic for the new component.
- **Content Example:**
    
    typescript
    
    ```ts
    import { Component } from '@angular/core';
    
    @Component({
      selector: 'app-new-component',
      templateUrl: './new-component.component.html',
      styleUrls: ['./new-component.component.css']
    })
    export class NewComponent {
      message = 'Hello from the new component!';
    }
    ```
    

**File: `new-component.component.html`**

- **Purpose:** Contains the HTML template for the new component.
- **Content Example:**
    
    
    
    ```html
    <p>{{ message }}</p>
    ```
    

**File: `new-component.component.css`**

- **Purpose:** Contains the styles for the new component.
- **Content Example:**
    
    
    
    ```css
    p {
      color: blue;
    }
    ```
    

## Changing Style

Styles in Angular components can be applied through the `*.component.css` file or inline styles within the template.

**File: `app.component.css`**

- **Purpose:** Contains styles for the root component.
- **Content Example:**
    
    
    
   ```css
    h1  
    ```