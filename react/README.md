# digITs style guide for ReactJS v1

Note: The goal is to rewrite this style-guide when the [Gamma](https://github.com/cthit/gamma) project is completed and when the common components has been extraced from there. This style guides will be explained with the common components.

---

## Table of Contents

1.  [Creation of a new project](#creation-of-a-new-project)
2.  [Different kinds of components](#different-kinds-of-components)
3.  [File naming](#file-naming)
4.  [Folder structure](#folder-structure)
5.  [Code structure](#code-structure)
6.  [Tools](#tools)

---

## Creation of a new project

[Create-react-app](https://github.com/facebook/create-react-app) should always be the starting project of any new ReactJS project.

If you're unsure about the tools used or ReactJS generally, then you shouldn't be the one setting up the project or initalizing the different tools. Ask someone who has experince. It's often easier to see how someone else does something and try to mimic that instead of starting on your own and trying to follow this styleguide.

---

## Different kinds of components

### Element

An element is a stateless and [pure](https://en.wikipedia.org/wiki/Pure_function) component that should only focus on presentational matters. They should take in props, and display it. An element may contain other elements, but not other views, screens or use-cases. An element should not use any hooks since it's [pure](https://en.wikipedia.org/wiki/Pure_function). It should always to a functional component, not a class component.

Two examples for elements would be the following:

-   A Button: It takes in text for the button and an onClick function to call when the button has been pressed.
-   A TextField: It takes in the value of the textfield and a onChange function to call when the textfield changes. Note that the textfield doens't have a state to store the current value. That job is for a view.

### View

A view can be a class component or a functional component with hooks. It may contain other views or [elements](#element), but not contain [screens](#screen) or [use-cases](#use-case).

An example for what a view could be:

-   A LoginForm: A view that has multiple textfields and saves the state of them.

### Screen

A screen is a component that takes up the whole screen, except the navigation. It may contain [views](#view) and [elements](#element), but it may not contain a [use-case](#use-case). There must always be atleast one screen for every [use-case](#use-case).

Two examples for what screens can be:

-   Login: A simple screen that contains a LoginForm.
-   Users, UserDetail: Two screens that is a part of the [use-case](#use-case) Users.

### Use-case

Your web application will contain several use-cases, who in their turn will contain the different screens. A use-case can, for example, be a 'Users'. This use-case manages the creation, editing, deletion, and viewing of users. This is a neat way of structuring your project.

---

## File naming

For each folder, including use-cases, screens, views and elements, can, but must not, contain these types of files:

`index.js`, should contain the export of the Component file. If there's a container however, it should export that instead. index.js is used to you only have to import the folder, not a specific file inside the folder.

`Component.jsx`, the main component.

`Component.styles.jsx`, has all the styling for the component. e.g. [styled-components](#styled-components).

`Component.action-creator.jsx`, has all the action-creators for Component. e.g. [Redux](#redux).

`Component.actions.jsx`, has all the actions for the Component. e.g. [Redux](#redux).

`Component.reducer.jsx`, has the reducer for the Component. e.g. [Redux](#redux).

`Component.translations.json`, has the translations data for the Component.

### If a Component is a Screen, View, Element or if it's a util file

Then you should add what it is after the name of the component.

`Component.view.jsx`

`Component.element.styles.jsx`

`Component.screen.action-creator.jsx`

`id.generator.js`

### Hooks

If the name of the hook is `useTranslations`, then the file should be `use-translations.js`.

### File extension

The file extension should either be .json, .jsx or .js. .js should only be used for index.js and hooks. .json should only be used for translations. .jsx should be used for the rest.

---

## Folder structure

Within the src folder, there should only be three folders. [Common](#common), [Common-ui](#common-ui), [Use-cases](#use-cases) and [App](#app).

### Common

Common should components or other utility files which are used by two or more [Use-case](#use-cases). Common should contain the following folders:

-   **Views**

Filled with common views. See [View](#view).

-   **Elements**

Filled with common elements. See [Element](#element).

### Common-ui

There should only be three subfolders. Common-ui should only contain [Styled-components](#styled-components).

-   **design**

Basically design that doesn't need to have a JS component. E.g. css or styled-components.

-   **layout**

Useful components for laying out your web application.

-   **text**

Should contain Title, subtitle, text etc.

### Use-cases

A folder of use-cases. See [Use-case](#use-case).

### App

The folder that contains App.jsx.

### Api

A folder that contains _all_ requests. The full structure for the api folder can be seen below, but here's an explanation for each file:

`action-creator.users.api.js`, has redux actions, for e.g. getting users. Will use `delete.`, `get.`, `put.` and `post.` in the same folder.

`actions.users.api.js`, has all the different actions strings

`delete.users.api.js`, has the http requests for deleting users

`get.users.api.js`, has the http requests for retrieving users

`post.users.api`, has the http requests to add new users

`put.users.api`, has the http requests to change existing users

`props.users.api`, has all the different props that an user object can have. This is used to reduce the possibility of misspelling.

### Example

```
├── index.js <-- The starting point
├── app
│   ├── App.jsx
│   ├── App.styles.jsx
│   └── index.js
├── api
|    └── users
|       ├── action-creator.users.api.js
|       ├── actions.users.api.js
|       ├── delete.users.api.js
|       ├── get.users.api.js
|       ├── put.users.api.js
|       ├── post.users.api.js
|       ├── props.users.api.js
├── common
|       ├── put.users.api.js
│   ├── elements
│   │   └── button
│   │       ├── Button.element.jsx
│   │       ├── Button.element.styles.jsx
│   │       └── index.js
│   └── views
│       └── navigation
│           ├── elements
│           │   └── navigation-item
│           │       ├── index.js
│           │       ├── NavigationItem.element.container.jsx
│           │       ├── NavigationItem.element.jsx
│           │       └── NavigationItem.element.styles.jsx
│           ├── index.js
│           ├── Navigation.view.container.jsx
│           ├── Navigation.view.jsx
│           ├── Navigation.view.styles.jsx
│           └── Navigation.view.translations.json
├── common-ui
│   ├── design
│   │   ├── Design.styles.jsx
│   │   └── index.js
│   ├── layout
│   │   ├── index.js
│   │   └── Layout.styles.jsx
│   └── text
│       ├── index.js
│       └── Text.styles.jsx
└── use-cases
    └── users
        ├── index.js
        ├── screens
        │   ├── show-users
        │   │   ├── index.js
        │   │   ├── ShowUsers.screen.container.jsx
        │   │   ├── ShowUsers.screen.jsx
        │   │   ├── ShowUsers.screen.styles.jsx
        │   │   ├── ShowUsers.screen.translations.json
        │   │   └── views
        │   │       └── search
        │   │           ├── elements
        │   │           │   └── search-field
        │   │           │       ├── index.js
        │   │           │       ├── SearchField.element.jsx
        │   │           │       └── SearchField.element.styles.jsx
        │   │           ├── index.js
        │   │           ├── Search.view.container.jsx
        │   │           ├── Search.view.jsx
        │   │           ├── Search.view.styles.jsx
        │   │           └── Search.view.translations.json
        │   └── user-details
        │       ├── index.js
        │       ├── UserDetails.screen.container.jsx
        │       ├── UserDetails.screen.jsx
        │       ├── UserDetails.screen.styles.jsx
        │       └── UserDetails.screen.translations.json
        ├── Users.action-creator.jsx
        ├── Users.actions.jsx
        ├── Users.jsx
        ├── Users.reducer.jsx
        ├── Users.translations.json
        ├── Users.translations.jsx
        └── views
            └── user
                ├── elements
                │   └── user-image
                │       ├── index.js
                │       ├── UserImage.element.container.jsx
                │       ├── UserImage.element.jsx
                │       ├── UserImage.element.styles.jsx
                │       └── UserImage.translations.json
                ├── index.js
                ├── User.view.container.jsx
                ├── User.view.jsx
                ├── User.view.styles.jsx
                └── User.view.translations.json
```

---

## Code structure

These are some pattern or principles that you should follow when programming.

### Use prettier

Use [prettier](https://prettier.io/) to format your code. The offical config file for digIT can be found here: https://github.com/cthit/style-guides/blob/master/react/.prettierrc

### Functional components with hooks over class components

Using hooks makes sharing logic throughout the project easier. Use them.

## Tools

These are some of the recommended tools to use when developing in ReactJS. They are not mandatory, e.g. Redux is not needed for a simple project. Note that this style guide doesn't explain how these tools work, instead there's a link to a good resource to learn the different tools. I have removed libraries that react-digit-components implement since they will not be exposed to your website.

### react-digit-components

React-digit-components should absolutly be used if you're developing a product for digIT. It can be found [here](https://github.com/cthit/react-digit-components).

### Styled-components

[Styled-components](https://www.styled-components.com/) is an awesome way to style your components! This resource is all you need to get started with styled-components. The way you learn to actually use styled-components is by trial and error. It's a very easy tool.

-   [Getting started with styled-components](https://www.styled-components.com/#your-first-styled-component)

### React-router-dom

[React-router-dom](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom) is an absolute must if you have more than one page. Lucily, it's the easiest tool of them all. Here's a great resource to get started with react-router-dom.

-   [Basic intro to React Router](https://medium.com/@thejasonfile/basic-intro-to-react-router-v4-a08ae1ba5c42)

When using react-router-dom, the only components you'll need, if you're using react-digit-components, is the `Switch` and `Route`. The rest is implemented by react-digit-components.

### Axios

[Axios](https://github.com/axios/axios) should be used instead of fetch. Reasonings why can be found [here](https://medium.com/@sahilkkrazy/fetch-vs-axios-http-request-c9afa43f804e).

### Yup

[Yup](https://github.com/jquense/yup) is also an awesome tool to easily validate the forms from react-digit-components.

### Context

An easy way to share state between components. Also works great with hooks. Context is much easier than Redux.

-   [Introduction to Context](https://reactjs.org/docs/context.html)
-   [Context and hooks](https://reactjs.org/docs/hooks-reference.html#usecontext)

### Redux

If you want to learn Redux, you should read these three link througly. These are all official guides on how to use Redux, and absolutly the best one out there.

-   [Introduction to Redux](https://redux.js.org/introduction)
-   [Basics](https://redux.js.org/basics)
-   [Advanced](https://redux.js.org/advanced)

Redux is great to handle state within a web application, and should be used whenever a complex application is in the making. If you need to make multiple HTTP requests and send that data throughout the web application, you should use Redux. Redux now has hooks, they are cool!
