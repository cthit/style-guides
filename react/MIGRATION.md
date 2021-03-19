# From `v1` to `v2`

The name of the game for v2 is simplification. 

## Merge `view` and `element` to `component`

The main motivation of seperating views and elements was to seperate class components and function components. But two problem arose from this solution:

* When entering a new project, it wasn't clear where one could find a given react component. Was it a component that had state or not? Was it an element that was within a view? 
* When React introduced hooks, everything changed. And so did the confusion with diffenciating between views and elements. Was an element that just had a `useMemo` hook still an element? Or was it now a view?

`v2` refocuses on instead on the user thinking on having components Single-responsibility principle. 

Please note that terms such as `use-case` and `screen` remains. They are still a good way of seperating large portions of a project.

## Do not use Redux

Redux can be a great solution for large scale React web applications. But rarely, if ever, does digITs websites reach the complexity that makes Redux worth it. Redux often introduced a lot of headache for people just learning web development. It was a obstacle to just getting started.

If you need to share state inside your application in a larger scale, contexts with hooks are great. An easier example is how translations are implemented in [cthit/react-digit-components](https://github.com/cthit/react-digit-components), which you can see [here](https://github.com/cthit/react-digit-components/blob/ab8a912df0cd63e59d24e7e848cabd477b0826ba/src/contexts/DigitTranslationsContext.js). The application is wrapped [here](https://github.com/cthit/react-digit-components/blob/ab8a912df0cd63e59d24e7e848cabd477b0826ba/src/declaratives/digit-providers/DigitProviders.declarative.jsx#L60) and can be access via a helper hook like [this](https://github.com/cthit/react-digit-components/blob/ab8a912df0cd63e59d24e7e848cabd477b0826ba/src/hooks/use-digit-translations.js#L24).

The [README.md](README.md) also has an easier example for the above pattern.

If you're still interested in Redux, check out the [Redux Toolkit](https://redux-toolkit.js.org/) that has good defaults for using Redux.

## `react-digit-components` is finally stable

[There's](https://mat.chalmers.it) [now](https://gamma.chalmers.it) [many](https://findit.chalmers.it) [websites](https://songbook.chalmers.it) [that's](https://suggestit.chalmers.it) [using](https://linkit.chalmers.it) [react-digit-components](https://eatit.chalmers.it). `v1` has been released and the documentation is stable. The biggest drawback is still how locked the styling becomes.

## Remove `.styles.jsx` files and `common-ui`. Keep styling more tightly connected to individual components

Using `common-ui` can sometimes mean that your application becomes highly coupled in the wrong ways. Having a seperate `.styles.jsx` could also make your application harder to read and get a good over. 

Defining a couple of helper styled-components in the same file as a component make it easy to get an exact overview of what exactly is happening inside the component. If you're having problem with having too many styled-components, then maybe that given components is breaking the Single-responsibility principle.

## Remove `sub-views` and `sub-elements`. Instead just create the sub component folders in the same folder.

Example, from:

```
`-- table
    |-- index.js
    |-- Table.element.jsx
    `-- sub-elements
        `-- table-row
            |-- TableRow.element.jsx
            `-- index.js
```

to

```
`-- table
    |-- index.js
    |-- Table.element.jsx
    `-- table-row
        |-- TableRow.element.jsx
        `-- index.js
```

The extra folder doesn't really give any new information. A new folder inside a folder is already an indication that there's a sub component inside that's relevant to the component.
