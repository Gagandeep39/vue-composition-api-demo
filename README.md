# Vue Composition API

- [Vue Composition API](#vue-composition-api)
  - [Deployment](#deployment)
  - [Description](#description)
  - [Composition API Details](#composition-api-details)
  - [Demo](#demo)

## Deployment

- Checkout deployment at <https://gagandeep39.github.io/vue-composition-api-demo/>

## Description

- There are 2 ways of writing vue components
  - Options API (Traditional)
  - Compositions API

## Composition API Details

- Alternative way of writing Vue Logic
- Used for Larger Apps
- Main problem with large apps: Too much data and UI code in large apps
- In options API, lot of similar code that should belong together is split across dofferent parts such as watcher, methods, computed etc.
- Composition API allows reusing logic
- Basically merging `data()`, `methods`, `computed`, `watch` into `setup()`

## Demo

- Ref iis used to srtore reactive value
- It work similar to watcher
- It updates variable when inside value changes
- Return statement contains value that can be sued in tmeplate
- Here `username` is an object that tores dynamic data
- We can assign value without ref, but it will not be dynamic ie changes ill not be renderded on UI
- To updte data, we have to ccess it using `.value`

```js
import { ref } from 'vue';

export default {
  setup() {
    const username = ref('Gagandeep');
    // Return all data we want to expose to template
    setTimeout(() => {
      username.value = 'POkemon';
    }, 100);
    return { username };
  },
};
```

```js
// Using ref for complex object
export default {
  setup() {
    const username = ref('Gagandeep');
    const obj = ref({ name: 'Gagan', age: 21 });
    console.log(username);
    // Return all data we want to expose to template

    setTimeout(() => {
      username.value = 'POkemon';
      obj.value.name = 'Gagandeep';
    }, 100);
    return { username, obj };
  },
};
```

```html
<!-- Accessing data -->
<div>
  <p>{{ username }}</p>
  <p>{{ obj.name }}</p>
</div>
```
