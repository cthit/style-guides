# digITs style guide for ReactJS v2

For migration between style guides, please see [MIGRATION.md](MIGRATION.md).

---

## Table of Contents

1.  [Creation of a new project](#creation-of-a-new-project)
2.  [Different kinds of components](#different-kinds-of-components)
3.  [File naming](#file-naming)
4.  [Translations](#translations)
4.  [Folder structure](#folder-structure)
5.  [Tools](#tools)

---

## Creation of a new project

[Create-react-app](https://github.com/facebook/create-react-app) should always be the starting project of any new ReactJS project.

If you're unsure about the tools used or ReactJS generally, then you shouldn't be the one setting up the project or initializing the different tools. Ask someone who has experience. It's often easier to see how someone else does something and try to mimic that instead of starting on your own and trying to follow this style guide.

---

## Different kinds of components


### Use-case

Your web application will contain several use-cases, which in their turn can contain different screens. A use-case can, for example, be a 'Users'. This use-case manages the creation, editing, deletion, and viewing of users. This is a neat way of structuring your project.

### Screen

A screen is a component that takes up the whole screen, except the navigation. It may contain [components](#components), but it may not contain a [use-case](#use-case).

Two examples for what screens can be:

-   Login: A simple screen that contains a component LoginForm.
-   ShowUsers, UserDetail: Two screens that are a part of the [use-case](#use-case) Users.


### Component

A component is everything that's not a [use-case](#use-case) or [screen](#screen). The only important thing to remember is to give a component only responsibility for one thing. In other words, follow the Single-responsibility principle.

---

## File naming

Each folder, including use-cases, screens, and components, can, but must not, contain these types of files:

* `index.js`, should contain the export of the `*.jsx` file. If there's a container, however, it should export that instead. index.js is used to you only have to import the folder, not a specific file inside the folder.

* `MyUseCase.jsx` / `MyScreen.screen.jsx` / `MyComponent.comp.jsx`: the main element.

* `Element.translations.json`/`Element.(screen/comp).translations.json`: has the translation data for the Element.

### Hooks

If the name of the hook is `useTranslations`, then the file should be `use-translations.js`.

### File extension

`.js` should only be used for `index.js` and hooks. `.json` should only be used for translations. `.jsx` should be used for the rest.

---

## Translations

There are three ways of implementing translations in your app:

1. Have one big `Translations.json` file with all translations.
2. Have a `CommonTranslations.json` file common translations such "Cancel" or "Save", and one `*.json` file per `use-case`. 
3. Still have a `CommonTranslation.json`, but have `*.json` everywhere, for every use-case, screen, or component per basis. I.e. a `Button.comp.translations.json` for translations for a Button.

There isn't a correct answer, the important part is just to be consistent. Using `*.json` works great with `react-digit-components`'s `useDigitTranslations()` hook.

---

## Folder structure

Within the src folder, there should only be five folders. [Common](#common), [Use-cases](#use-case), [App](#app) and [api](#api).

### Common

Common should components or other utility files which are used by two or more [Use-case](#use-case). Common should contain the following folders:

-   **components**

-   **hooks**

-   **contexts**

### Use-cases

A folder of use-cases. See [Use-case](#use-case).

### App

The folder that contains App.jsx.

### Api

A folder that contains _all_ requests. The full structure for the api folder can be seen below, but here's an explanation for each file:

`delete.users.api.js`, has the http requests for deleting users

`get.users.api.js`, has the http requests for retrieving users

`post.users.api`, has the http requests to add new users

`put.users.api`, has the http requests to change existing users

It can also be useful to have `utils.js` and `endpoints.js` in the root folder of `api`. 


### Example

```
src
 ├── index.js <-- The starting point, having ReactDom.render...
 ├── app
 │   ├── App.jsx
 │   └── index.js
 ├── api
 |    ├── utils.js
 |    ├── endpoints.js 
 |    └── users
 |       ├── delete.users.api.js
 |       ├── get.users.api.js
 |       ├── put.users.api.js
 |       └── post.users.api.js
 ├── common
 │   └── components
 │       ├── button
 │       │     ├── Button.comp.jsx
 │       │     └── index.js
 │       └── navigation
 │           ├── navigation-item
 │           │       ├── index.js
 │           │       └── NavigationItem.comp.jsx
 │           ├── index.js
 │           ├── Navigation.comp.jsx
 │           └── Navigation.comp.translations.json
 └── use-cases
     └── users
         ├── index.js
         ├── Users.jsx
         ├── Users.translations.json
         ├── screens
         │   ├── show-users
         │   │   ├── index.js
         │   │   ├── ShowUsers.screen.jsx
         │   │   ├── ShowUsers.screen.translations.json
         │   │   └── search
         │   │       ├── search-field
         │   │       │   ├── index.js
         │   │       │   └── SearchField.comp.jsx
         │   │       ├── index.js
         │   │       ├── Search.comp.jsx
         │   │       └── Search.comp.translations.json
         │   └── user-details
         │       ├── index.js
         │       ├── UserDetails.screen.jsx
         │       └── UserDetails.screen.translations.json
         └── components
             └── user
                 ├── user-image
                 │     ├── index.js
                 │     ├── UserImage.comp.jsx
                 │     └── UserImage.comp.translations.json
                 ├── index.js
                 ├── User.comp.jsx
                 └── User.comp.translations.json
```

---


## Tools

These are some of the recommended tools to use when developing ReactJS. They are not mandatory. Note that this style guide doesn't explain how these tools work, instead there's a link to a good resource to learn the different tools. I have removed libraries that react-digit-components implement since they will not be exposed to your website.

### Use prettier

Use [prettier](https://prettier.io/) to format your code. The official config file for digIT can be found [here](https://github.com/cthit/style-guides/blob/master/react/.prettierrc)

### react-digit-components

React-digit-components should absolutely be used if you're developing a product for digIT. It can be found [here](https://github.com/cthit/react-digit-components).

### Styled-components

[Styled-components](https://www.styled-components.com/) is an awesome way to style your components! This resource is all you need to get started with styled-components. The way you learn to actually use styled-components is by trial and error. It's a very easy tool.

-   [Getting started with styled-components](https://www.styled-components.com/#your-first-styled-component)

### React-router-dom

[React-router-dom](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom) is an absolute must if you have more than one page. Luckily, it's the easiest tool of them all. Here's a great resource to get started with react-router-dom.

-   [Basic intro to React Router](https://medium.com/@thejasonfile/basic-intro-to-react-router-v4-a08ae1ba5c42)

When using react-router-dom, the only components you'll need, if you're using react-digit-components, are the `Switch` and `Route`. The rest is implemented by react-digit-components.

### Axios

[Axios](https://github.com/axios/axios) should be used instead of fetch. Reasonings why can be found [here](https://medium.com/@sahilkkrazy/fetch-vs-axios-http-request-c9afa43f804e).

### Yup

[Yup](https://github.com/jquense/yup) is also an awesome tool to easily validate the forms from react-digit-components.

### Context

An easy way to share state between components. 

-   [Introduction to Context](https://reactjs.org/docs/context.html)
-   [Context and hooks](https://reactjs.org/docs/hooks-reference.html#usecontext)

A great pattern to easily access state across your web app is:

* Singleton provider to provide the context to the entire app:

```jsx
import React, { createContext, useState } from "react";
const MainStateContext = createContext({});

const MainStateContextSingletonProvider = ({ children }) => {
    const [state, setState] = useState({});

    return (
        <MainStateContext.Provider value={[state, setState]}>
            {children}
        </MainStateContext.Provider>
    );
};

export { MainStateContextSingletonProvider };
export default MainStateContext;
```

* Wrapping your app in a Single provider:

Inside your main `index.js`, you would have something like this:

```jsx

import React from "react";
import ReactDOM from "react-dom";
import App from "./app";
import { MainStateContextSingletonProvider } from "...";

ReactDOM.render(
    <MainStateContextSingletonProvider>
        <App />
    </MainStateContextSingletonProvider>,
    document.getElementById("root")
);

```

* `useMainState` hook:

Having a layer between your components and your context can provide you easy access to fix default cases in your hook. You can also easier change the source of the data without having to change how the hook is handled.

```jsx

import { useContext } from "react";
import MainStateContext from "../contex# digITs style guide for ReactJS v2

For migration between style guides, please see [MIGRATION.md](MIGRATION.md).

---

## Table of Contents

1.  [Creation of a new project](#creation-of-a-new-project)
2.  [Different kinds of components](#different-kinds-of-components)
3.  [File naming](#file-naming)
4.  [Translations](#translations)
4.  [Folder structure](#folder-structure)
5.  [Tools](#tools)

---

## Creation of a new project

[Create-react-app](https://github.com/facebook/create-react-app) should always be the starting project of any new ReactJS project.

If you're unsure about the tools used or ReactJS generally, then you shouldn't be the one setting up the project or initalizing the different tools. Ask someone who has experince. It's often easier to see how someone else does something and try to mimic that instead of starting on your own and trying to follow this styleguide.

---

## Different kinds of components


### Use-case

Your web application will contain several use-cases, who in their turn can contain different screens. A use-case can, for example, be 'Users'. This use-case manages the creation, editing, deletion, and viewing of users. This is a neat way of structuring your project.

### Screen

A screen is a component that takes up the whole screen, except the navigation. It may contain [components](#components), but it may not contain a [use-case](#use-case).

Two examples for what screens can be:

-   Login: A simple screen that contains a component LoginForm.
-   ShowUsers, UserDetail: Two screens that is a part of the [use-case](#use-case) Users.


### Component

A component is everything that's not a [use-case](#use-case) or [screen](#screen). The only important thing to remember is to give a component only responibility for one thing. In other words, follow the Single-responsibility principle.

---

## File naming

For each folder, including use-cases, screens, views and elements, can, but must not, contain these types of files:

* `index.js`, should contain the export of the `*.jsx` file. If there's a container however, it should export that instead. index.js is used to you only have to import the folder, not a specific file inside the folder.

* `Element.jsx`, the main element.

* `Element.translations.json`, has the translations data for the Element.

### Hooks

If the name of the hook is `useTranslations`, then the file should be `use-translations.js`.

### File extension

`.js` should only be used for `index.js` and hooks. `.json` should only be used for translations. `.jsx` should be used for the rest.

---

## Translations

There's three ways of implementing translations in your app:

1. Have one big `Translations.json` file with all translations.
2. Have a `CommonTranslations.json` file common translations such "Cancel" or "Save", and one `*.json` file per `use-case`. 
3. Still have a `CommonTranslation.json`, but have `*.json` everywhere it's needed.

There isn't a correct answer, the important part is just to be consistent. Using `*.json` works great with `react-digit-components`'s `useDigitTranslations()` hook.

---

## Folder structure

Within the src folder, there should only be five folders. [Common](#common), [Use-cases](#use-case), [App](#app) and [api](#api).

### Common

Common should components or other utility files which are used by two or more [Use-case](#use-case). Common should contain the following folders:

-   **components**

-   **hooks**

-   **contexts**

### Use-cases

A folder of use-cases. See [Use-case](#use-case).

### App

The folder that contains App.jsx.

### Api

A folder that contains _all_ requests. The full structure for the api folder can be seen below, but here's an explanation for each file:

`delete.users.api.js`, has the http requests for deleting users

`get.users.api.js`, has the http requests for retrieving users

`post.users.api`, has the http requests to add new users

`put.users.api`, has the http requests to change existing users

It can also be useful to have a `utils.js` and `endpoints.js` in the root folder of `api`. 


### Example

```
src
 ├── index.js <-- The starting point, having ReactDom.render...
 ├── app
 │   ├── App.jsx
 │   └── index.js
 ├── api
 |    ├── utils.js
 |    ├── endpoints.js 
 |    └── users
 |       ├── delete.users.api.js
 |       ├── get.users.api.js
 |       ├── put.users.api.js
 |       └── post.users.api.js
 ├── common
 │   └── components
 │       ├── button
 │       │     ├── Button.comp.jsx
 │       │     └── index.js
 │       └── navigation
 │           ├── navigation-item
 │           │       ├── index.js
 │           │       └── NavigationItem.comp.jsx
 │           ├── index.js
 │           ├── Navigation.comp.jsx
 │           └── Navigation.comp.translations.json
 └── use-cases
     └── users
         ├── index.js
         ├── Users.jsx
         ├── Users.translations.json
         ├── screens
         │   ├── show-users
         │   │   ├── index.js
         │   │   ├── ShowUsers.screen.jsx
         │   │   ├── ShowUsers.screen.translations.json
         │   │   └── search
         │   │       ├── search-field
         │   │       │   ├── index.js
         │   │       │   └── SearchField.comp.jsx
         │   │       ├── index.js
         │   │       ├── Search.comp.jsx
         │   │       └── Search.comp.translations.json
         │   └── user-details
         │       ├── index.js
         │       ├── UserDetails.screen.jsx
         │       └── UserDetails.screen.translations.json
         └── components
             └── user
                 ├── user-image
                 │     ├── index.js
                 │     ├── UserImage.comp.jsx
                 │     └── UserImage.comp.translations.json
                 ├── index.js
                 ├── User.comp.jsx
                 └── User.comp.translations.json
```

---


## Tools

These are some of the recommended tools to use when developing in ReactJS. They are not mandatory. Note that this style guide doesn't explain how these tools work, instead there's a link to a good resource to learn the different tools. I have removed libraries that react-digit-components implement since they will not be exposed to your website.

### Use prettier

Use [prettier](https://prettier.io/) to format your code. The offical config file for digIT can be found [here](https://github.com/cthit/style-guides/blob/master/react/.prettierrc)

### react-digit-components

React-digit-components should absolutly be used if you're developing a product for digIT. It can be found [here](https://github.com/cthit/react-digit-components).

### Styled-components

[Styled-components](https://www.styled-components.com/) is an awesome way to style your components! This resource is all you need to get started with styled-components. The way you learn to actually use styled-components is by trial and error. It's a very easy tool.

-   [Getting started with styled-components](https://www.styled-components.com/#your-first-styled-component)

### React-router-dom

[React-router-dom](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom) is an absolute must if you have more than one page. Luckily, it's the easiest tool of them all. Here's a great resource to get started with react-router-dom.

-   [Basic intro to React Router](https://medium.com/@thejasonfile/basic-intro-to-react-router-v4-a08ae1ba5c42)

When using react-router-dom, the only components you'll need, if you're using react-digit-components, is the `Switch` and `Route`. The rest is implemented by react-digit-components.

### Axios

[Axios](https://github.com/axios/axios) should be used instead of fetch. Reasonings why can be found [here](https://medium.com/@sahilkkrazy/fetch-vs-axios-http-request-c9afa43f804e).

### Yup

[Yup](https://github.com/jquense/yup) is also an awesome tool to easily validate the forms from react-digit-components.

### Context

An easy way to share state between components. 

-   [Introduction to Context](https://reactjs.org/docs/context.html)
-   [Context and hooks](https://reactjs.org/docs/hooks-reference.html#usecontext)

A great pattern to easily access state across your web app is:

* Singleton provider to provide the context to the entire app:

```jsx
import React, { createContext, useState } from "react";
const MainStateContext = createContext({});

const MainStateContextSingletonProvider = ({ children }) => {
    const [state, setState] = useState({});

    return (
        <MainStateContext.Provider value={[state, setState]}>
            {children}
        </MainStateContext.Provider>
    );
};

export { MainStateContextSingletonProvider };
export default MainStateContext;
```

* Wrapping your app in the Single provider:

Inside your main `index.js`, you would have something like this:

```jsx

import React from "react";
import ReactDOM from "react-dom";
import App from "./app";
import { MainStateContextSingletonProvider } from "...";

ReactDOM.render(
    <MainStateContextSingletonProvider>
        <App />
    </MainStateContextSingletonProvider>,
    document.getElementById("root")
);

```

* `useMainState` hook:

Having a layer between your components and your context can provide you easy access to fix default cases in your hook. You can also easier change the source of the data without having to change how the hook is handled.

```jsx

import { useContext } from "react";
import MainStateContext from "../contexts/MainStateContext";

function useMainState() {
    const [state, setState] = useContext(MainStateContext);

    return [state, setState];
}

export default useMainState;

```

You can now easily access this main state with the hook:

```jsx

const [state, setState] = useMainState();

```

Please note the difference in export for the SingleProvider.

If you want an example when using `useReducer` instead, you can find a good example [here](https://github.com/cthit/react-digit-components/blob/c8b4e46230f2b080d9ccda8c7f31e2148f679b31/src/contexts/DigitTranslationsContext.js#L7).t(MainStateContext);

    return [state, setState];
}

export default useMainState;

```

You can now easily access this main state with the hook:

```jsx

const [state, setState] = useMainState();

```

Please note the difference in export for the SingleProvider.

If you want an example when using `useReducer` instead, you can find a good example [here](https://github.com/cthit/react-digit-components/blob/c8b4e46230f2b080d9ccda8c7f31e2148f679b31/src/contexts/DigitTranslationsContext.js#L7).
