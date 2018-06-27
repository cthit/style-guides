# digITs style guide for ReactJS

Note: The goal is to rewrite this style-guide when the [Gamma](https://github.com/cthit/gamma) project is completed and when the common components has been extraced from there. This style guides will be explained with the common components.

<hr>

## Table of Contents

1.  [Code format](#code-format)
2.  [Creation of a new project](#creation-of-a-new-project)
3.  [Tools](#tools)
4.  [Different kinds of components](#different-kinds-of-components)
5.  [Folder structure](#folder-structure)
6.  [Code structurer](#code-structure)
7.  [File naming](#file-naming)

<hr>

## Code format

- Use [prettier](https://prettier.io/) to format your code.

<hr>

## Creation of a new project

[Create-react-app](https://github.com/facebook/create-react-app) should always be the starting project of any new ReactJS project.

If you're unsure about the tools used or ReactJS generally, then you shouldn't be the one setting up the project or initalizing the different tools. Ask someone who has experince. It's often easier to see how someone else does something and try to mimic that instead of starting on your own and trying to follow this styleguide.

<hr>

## Tools

These are some of the recommended tools to use when developing in ReactJS. They are not mandatory, e.g. Redux is not needed for a simple project. Note that this style guide doesn't explain how these tools work, instead there's a link to a good resource to learn the different tools.

### Redux

If you want to learn Redux, you should read these three link througly. These are all official guides on how to use Redux, and absolutly the best one out there.

- [Introduction to Redux](https://redux.js.org/introduction)
- [Basics](https://redux.js.org/basics)
- [Advanced](https://redux.js.org/advanced)

Redux is great to handle state within a web application, and should be used whenever a complex application is in the making. If you need to make multiple HTTP requests and send that data throughout the web application, you should use Redux.

### Styled-components

[Styled-components](https://www.styled-components.com/) is an awesome way to style your components! This resource is all you need to get started with styled-components. The way you learn to actually use styled-components is by trial and error. It's a very easy tool.

- [Getting started with styled-components](https://www.styled-components.com/#your-first-styled-component)

### React-router-dom

[React-router-dom](https://github.com/ReactTraining/react-router/tree/master/packages/react-router-dom) is an absolute must if you have more than one page. Lucily, it's the easiest tool of them all. Here's a great resource to get started with react-router-dom.

- [Basic intro to React Router](https://medium.com/@thejasonfile/basic-intro-to-react-router-v4-a08ae1ba5c42)

TODO: Add link on how we use react-router-dom.

### React-localize-redux

digIT must strive to make their application support both english and swedish. [React-localize-redux](https://ryandrewjohnson.github.io/react-localize-redux-docs/#getting-started) is a good tool to do this.

- [If you're not using Redux](https://ryandrewjohnson.github.io/react-localize-redux-docs/)
- [If you're using Redux](https://ryandrewjohnson.github.io/react-localize-redux-docs/#what-if-i-want-to-use-redux)
- [Tools if you're using Redux](https://ryandrewjohnson.github.io/react-localize-redux-docs/#redux-helpers)

### Material-ui

[Material-ui](https://material-ui.com/) is react components that implements Google's Material Design. Future digIT library will make it much easier to use Material-ui in conjunktion with Styled-components. But if you want to learn how material-ui works for now you can use this resource:

### Axios

[Axios](https://github.com/axios/axios) should be used instead of fetch. Reasonings why can be found [here](https://medium.com/@sahilkkrazy/fetch-vs-axios-http-request-c9afa43f804e).

### Formik

[Formik](https://github.com/jaredpalmer/formik) is an awesome tool to create forms.

### Yup

[Yup](https://github.com/jquense/yup) is also an awesome tool to easily validate the forms from Formik. But it's not limited to Formik.

### lodash

[lodash](https://lodash.com/) contains a bunch of util functions.

<hr>

## Different kinds of components

### Element

An element is a stateless component that should only focus on presentational matters. They should take in props, and display it. An element may be compared to a [presentational component](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0). An element may contain other elements, but not other views, screens or use-cases.

Two examples for elements would be the following:

- A ButtonElement: It takes in text for the button and an onClick function to call when the button has been pressed.
- A TextFieldElement: It takes in the value of the textfield and a onChange function to call when the textfield changes. Note that the textfield doens't have a state to store the current value. That job is for a view. (Tips is to use [Formik](#formik) here)

### View

A view is a component is a bit versatile in contrary to the rules of [Element](#element), [Screen](#screen) and [Use-case](#use-case). A view may have a state or not. View may contain other views and element. However, it may not contain screens or use-cases. View may be compared to a [container component](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0).

An example for what a view could be:

- A LoginFormView: A view that has multiple textfields and saves the state of them. When the form is done, a button is used to send that information.

### Screen

A screen is a component that takes up the whole screen, except the navigation. It may contain views and elements, but it may not contain a use-case. There must always be atleast one screen on every use-case.

Two examples for what screens can be:

- LoginScreen: A simple screen that contains a LoginForm.
- UsersScreen, UserDetailScreen: Two screens that is a part of the use-case Users.

### Use-case

Your web application will contain several use-cases, who in their turn will contain the different screens.

<hr>

## Folder structure

Within the src folder, there should only be three folders. [Common](#common), [Common-ui](#common-ui), [Use-cases](#use-cases) and [App](#app).

### Common

Common should components or other utility files which are used by two or more [Use-case](#use-cases). Common should contain the following folders:

#### Views

Filled with common views. See [View](#view).

#### Elements

Filled with common elements. See [Element](#element).

#### Declaratives

Se [Declarative design](#declarative-design)

#### Utils

Utils should only contain functions or constants.

##### Constants

Useful constants.

##### Formatters

Should take in a unformatted input and return it formatted.

##### Generators

Should generate values, like ids for examples.

##### Loaders

Should load local files of some sort, for example translations.

##### Translations

Should contain .json data of translations.

##### Requests

Requests to a server. Should return promises.

### Common-ui

There should only be three subfolders. Common-ui should only contain [Styled-components](#styled-components).

#### design

Basically design that doesn't need to have a component.

#### layout

Useful components for laying out your web application.

#### text

Should contain Title, subtitle, text etc.

### Use-cases

A folder of use-cases. See [Use-case](#use-case).

### App

The folder that contains App.jsx.

<hr>

## Code structure

These are some pattern or principles that you should follow when programming.

### Declarative design

Try to always use declarative design when programming. If you have to use imperative programming, put it into a component in common/declarative so it can be reused.

### Deconstructors

Instead of using this.props or this.state in Components with state, use deconstructors.

<code>const { glass, godis } = this.props;</code>

### Order of imports

1.  From npm e.g. <code>import React from "react";</code>
2.  Imports from the same folder <code>import {StyledTextField} from "./InputCid.view.styles";</code>
3.  Imports from the same use-case, app, common or common-ui.
4.  Imports from the common folder.
5.  Imports from the common-ui folder.

<hr>

## File naming

For each folder, including use-cases, screens, views and elements, can, but must not, contain these types of files:

<code>index.js</code>

Should contain the export of the Component file. If there's a container however, it should export that instead. index.js is used to you only have to import the folder, not a specific file inside the folder.

<code>Component.jsx</code>

The main component.

<code>Component.styles.jsx</code>

Has all the styling for the component. (Styled-components).

<code>Component.action-creator.jsx</code>

Has all the action-creators for Component. (Redux).

<code>Component.actions.jsx</code>

Has all the actions for the Component. (Redux).

<code>Component.reducer.jsx</code>

Has the reducer for the Component. (Redux).

<code>Component.translations.json</code>

Has the translations data for the Component.

<code>Component.translations.jsx</code>

Only exists for use-cases. Collects all the translations.json from the screens, views and elements.

### If a Component is a Screen, View, Element or if it's a util file

Then you should add what it is after the name of the component. If it's a use-case, Example:

<code>Component.view.jsx</code>

<code>Component.element.styles.jsx</code>

<code>Component.screen.action-creator.jsx</code>

<code>id.generator.js</code>

<code>translations.loader.js</code>

### File extension

The file extension should either be .json, .jsx or .js. .js should only be used for index.js. .json should only be used for translations. .jsx should be used for the rest.
