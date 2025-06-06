# Vue.js Application API Reference

## Mounting Vue Application

Shows how to mount a Vue application instance to a DOM element using app.mount().  It imports createApp, creates an app instance (details omitted for brevity), and then mounts it to an element with the ID 'app'.  This initiates the rendering process, inserting the Vue component into the specified DOM element.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_2

```javascript
import { createApp } from 'vue'
const app = createApp(/* ... */)

app.mount('#app')
```

---

## Providing a Value for Injection (App-Level)

Demonstrates how to provide a value at the application level for dependency injection using app.provide(). It creates a Vue application instance and provides the string value 'hello' under the injection key 'message'. This makes the value available for injection in any descendant component within the application.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_10

```javascript
import { createApp } from 'vue'

const app = createApp(/* ... */)

app.provide('message', 'hello')
```

---

## Registering Global Component

Illustrates registering a global component using app.component(). It creates a Vue application instance and then registers a component named 'MyComponent' with a provided component options object. This makes the component available for use in any other component within the application.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_4

```javascript
import { createApp } from 'vue'

const app = createApp({})

// register an options object
app.component('MyComponent', {
  /* ... */
})
```

---

## Injecting Provided Value (Composition API)

Illustrates how to inject a provided value within a component using the Composition API and the inject function. It imports the inject function from 'vue' and injects the value associated with the 'message' key within the setup function, logging it to the console. This allows components to access values provided at the application level.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_11

```javascript
import { inject } from 'vue'

export default {
  setup() {
    console.log(inject('message')) // 'hello'
  }
}
```

---

## Registering Global Properties in Vue.js

This example demonstrates how to register global properties that can be accessed on any component instance inside the application.  This makes the property available inside any component template and on `this` of any component instance.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_21

```javascript
app.config.globalProperties.msg = 'hello'
```

```javascript
export default {
  mounted() {
    console.log(this.msg) // 'hello'
  }
}
```

---

## Configuring ID Prefix for useId() in Vue.js

This snippet shows how to configure a prefix for all IDs generated via `useId()` inside this application. The `idPrefix` setting provides a way to namespace IDs generated by `useId()`.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_23

```javascript
app.config.idPrefix = 'myApp'
```

```javascript
// in a component:
const id1 = useId() // 'myApp:0'
const id2 = useId() // 'myApp:1'
```

---

## Mounting Vue Application to DOM Element

Demonstrates mounting a Vue application to a specific DOM element reference using app.mount().  It gets a reference to the first child of the body element and then mounts the Vue application to that specific DOM node. This is an alternative to using a CSS selector.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_3

```javascript
app.mount(document.body.firstChild)
```

---

## Injecting Provided Value (Options API)

Demonstrates how to inject a provided value within a component using the Options API and the inject option. It defines an inject option that lists 'message' as an injection dependency and then accesses the injected value using `this.message` in the created lifecycle hook. This allows components to access values provided at the application level.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_12

```javascript
export default {
  inject: ['message'],
  created() {
    console.log(this.message) // 'hello'
  }
}
```

---

## Using a Plugin

Illustrates how to install a plugin into a Vue application using app.use().  It imports createApp from 'vue' and a plugin named 'MyPlugin' from './plugins/MyPlugin'. The plugin is then installed using app.use(MyPlugin), allowing the plugin to extend the application's functionality.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_9

```javascript
import { createApp } from 'vue'
import MyPlugin from './plugins/MyPlugin'

const app = createApp({
  /* ... */
})

app.use(MyPlugin)
```

---

## Setting Global Error Handler

Shows how to assign a global error handler using app.config.errorHandler. The error handler function receives the error, the component instance, and an information string as arguments and can be used to report errors to a service or perform other error handling tasks. This allows centralized error management for the entire Vue application.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_15

```javascript
app.config.errorHandler = (err, instance, info) => {
  // handle error, e.g. report to a service
}
```

---

## Registering Custom Directive (Function Shorthand)

Shows how to register a global custom directive using app.directive() with a function shorthand definition. It creates a Vue application instance and registers a directive named 'myDirective' using a function that will be executed when the directive is bound and updated. This provides a simpler way to define directives for basic use cases.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_7

```javascript
// register (function directive shorthand)
app.directive('myDirective', () => {
  /* ... */
})
```

---

## Defining Custom Option Merge Strategies in Vue.js

This example illustrates how to define a custom merge strategy for a component option.  A merge strategy function can be registered for a custom option by assigning it on the `app.config.optionMergeStrategies` object using the option's name as the key.  The example defines a custom merge strategy for `msg` that concatenates the parent and child values.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_22

```javascript
const app = createApp({
  // option from self
  msg: 'Vue',
  // option from a mixin
  mixins: [
    {
      msg: 'Hello '
    }
  ],
  mounted() {
    // merged options exposed on this.$options
    console.log(this.$options.msg)
  }
})

// define a custom merge strategy for `msg`
app.config.optionMergeStrategies.msg = (parent, child) => {
  return (parent || '') + (child || '')
}

app.mount('#app')
// logs 'Hello Vue'
```

---

## Running Callback with Application Context

Shows how to run a callback function with the current application's context using app.runWithContext(). It provides the value '1' for the 'id' key, then runs a function which injects and returns the 'id' value. This allows injecting values outside of a component's setup scope.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_13

```javascript
import { inject } from 'vue'

app.provide('id', 1)

const injected = app.runWithContext(() => {
  return inject('id')
})

console.log(injected) // 1
```

---

## Registering Custom Directive (Object Directive)

Demonstrates registering a global custom directive using app.directive() with an object-based directive definition. It creates a Vue application instance and registers a directive named 'myDirective' with a configuration object containing custom directive hooks. This enables custom DOM manipulation and logic during the component lifecycle.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_6

```javascript
import { createApp } from 'vue'

const app = createApp({
  /* ... */
})

// register (object directive)
app.directive('myDirective', {
  /* custom directive hooks */
})
```

---

## Setting isCustomElement Compiler Option in Vue.js

This example demonstrates setting the `isCustomElement` compiler option to recognize native custom elements. The function should return `true` if the tag should be treated as a native custom element. For a matched tag, Vue will render it as a native element instead of attempting to resolve it as a Vue component.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_17

```javascript
// treat all tags starting with 'ion-' as custom elements
app.config.compilerOptions.isCustomElement = (tag) => {
  return tag.startsWith('ion-')
}
```

---

## Retrieving Registered Component

Shows how to retrieve a globally registered component using app.component(). It gets the registered component 'MyComponent' and assigns it to a constant named 'MyComponent'.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_5

```javascript
// retrieve a registered component
const MyComponent = app.component('MyComponent')
```

---

## Initializing Vue Application (Imported Component)

Illustrates creating a Vue application with an imported root component using createApp.  It imports both createApp from 'vue' and a component named 'App' from './App.vue'.  The 'App' component is then passed as the first argument to createApp, creating the application instance.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_1

```javascript
import { createApp } from 'vue'
import App from './App.vue'

const app = createApp(App)
```

---

## Initializing Custom Warning Handler in Vue.js

This snippet shows how to assign a custom handler for runtime warnings from Vue. The handler receives the warning message, the source component instance, and a component trace string. It's useful for filtering out specific warnings during debug sessions in development mode.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_16

```javascript
app.config.warnHandler = (msg, instance, trace) => {
  // `trace` is the component hierarchy trace
}
```

---

## Preserving HTML Comments in Vue.js Templates

This snippet shows how to set the `comments` compiler option to `true` to force Vue to preserve HTML comments even in production. By default, Vue removes comments in production. This option is used when Vue is used with other libraries that rely on HTML comments.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_20

```javascript
app.config.compilerOptions.comments = true
```

---

## Initializing Vue Application (Inline Component)

Demonstrates creating a Vue application instance with an inline root component definition using the createApp function.  It imports createApp from 'vue' and defines a basic component options object directly within the createApp call. The resulting app instance is assigned to the 'app' constant.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_0

```javascript
import { createApp } from 'vue'

const app = createApp({
  /* root component options */
})
```

---

## Configuring Whitespace Handling in Vue.js Templates

This snippet illustrates setting the `whitespace` compiler option to `'preserve'` to disable whitespace condensation in templates. By default, Vue condenses whitespace for more efficient output. Setting this option to `'preserve'` will disable the removal and condensing of whitespace characters.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_18

```javascript
app.config.compilerOptions.whitespace = 'preserve'
```

---

## Retrieving Registered Directive

Demonstrates how to retrieve a globally registered directive using app.directive(). It retrieves the registered directive 'myDirective' and assigns it to a constant named 'myDirective'.

Source: https://github.com/vuejs/docs/blob/main/src/api/application.md#_snippet_8

```javascript
// retrieve a registered directive
const myDirective = app.directive('myDirective')
```

