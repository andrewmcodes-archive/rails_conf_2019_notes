# The Rails 6 Front End: Building with Webpacker and Stimulus

- [The Rails 6 Front End: Building with Webpacker and Stimulus](#the-rails-6-front-end-building-with-webpacker-and-stimulus)
  - [Stimulus](#stimulus)
    - [Controllers](#controllers)
    - [Actions](#actions)
    - [Target](#target)
    - [Map](#map)
    - [When to use](#when-to-use)
    - [Downsides](#downsides)
  - [Webpack](#webpack)
    - [Core functions](#core-functions)
    - [Entry](#entry)
    - [Output](#output)
    - [Loaders/Plugin](#loadersplugin)
    - [Webpacker](#webpacker)
  - [Misc](#misc)

## Stimulus

- [workshop snippets](https://gist.github.com/noelrappin/b87ee470f760d2496d2d03a0187a33f3)

### Controllers

- Where stimulus code is executed
- Associated with an html element
- Active across that element and its children
- An element can have multiple controllers
- Controller can be instantiated multiple times

### Actions

- JS event you are choosing to dispatch to controller
- Actions are associated with an html element
- Action associates an arbitrary event to a controller method
- The HTML element must be within the controller being referenced
- Camelcase

```js
event->controller#method

// Ex:
click->toggle#toggle

// flow
Click event -> toggle controller -> toggle action
```

### Target

- A target is an HTML element of interest to a controller
- Targets are associated with an HTML element
- Associated using `data-target`
- Camelcase
- Targets mae it easy to look up elements of interest
  - `this.thingToHideTarget`
  - `this.thingToHideTargets`
  - `this.hasThingToHideTarget`

### Map

Data maps belong to the controller

`data-controllername-key`

- get(key
- has(key)
- set()

### When to use

- Low overhead
- Easy to follow
- Removes a lot of boilerplate event listeners
- Makes it easy to write small modular effects
- Great at handling dynamic changes to the page

### Downsides

- No support for routers/spas
- Not super-helpful if there is a lot of state or controlled access to state

## Webpack

### Core functions

- Entry
- Output
- Loaders/Plugins

### Entry

- A file
- Often JS (in a Rails env)
- Usually referencing other files in use
- Uses entry points to build a "dependency graph"

### Output

- Where the bundle ends up
- Often the code is turned into a single file

### Loaders/Plugin

- Transform files
- Add them to the graph
- Adds files to list of dependencies that "need to get sent out"
- Uses babel
- Examples:
  - TypeScript compiler
  - CSS loader
  - File loader
- Most often used for some sort of compilation

### Webpacker

- Simplifies Webpack for Rails
- Provides useful defaults and makes some behaviors easier to override (at cost of making some other behavior harder to override)
- Default for Rails 6 apps over sprockets
- Default configs for:
  - Angular
  - Coffeescript 1
  - Typescript
  - Stimulus
  - Vue
  - ERB

## Misc

- [You might not need jQuery](http://youmightnotneedjquery.com)
