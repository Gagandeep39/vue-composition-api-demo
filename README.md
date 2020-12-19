# Vue Composition API

- [Vue Composition API](#vue-composition-api)
  - [Deployment](#deployment)
  - [Description](#description)
  - [Composition API Details](#composition-api-details)
  - [Demo](#demo)
    - [ref](#ref)
    - [reactive](#reactive)

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
- **If** we try to retun data as `obj.name`, then changes wont be seen in html, obj is a reactive object, however its children are not. Hence we have to return the whole `obj` to show changes dynamically
- **NOTE** `ref()` is for single value, `reactive()` is for object

```js
import { isReactive, isRef, reactive, ref, toRefs } from 'vue';

export default {
  setup() {
    // Refs
    const username = ref('Gagandeep');
    const obj = ref({ name: 'Gagan', age: 21 });
    // ###########  Ref  #############
    // Accessing object
    console.log(obj);
    console.log(obj.value.name);
    // Checkiing if it is reactive
    console.log(isRef(obj)); // True
    console.log(isRef(obj.value.name)); // False
    // ###########  Reactive  #############
    // Reactive
    const obj2 = reactive({ name: 'Gagan', age: 21 });
    // Accessing object
    console.log(obj2);
    console.log(obj2.name);
    // Checkiing if it is reactive
    console.log(isReactive(obj2)); // True
    console.log(isReactive(obj2.name)); // False
    // Making nested variable reactive (ref)
    const refObj = toRefs(obj2);
    console.log(isRef(refObj.name)); // true
    return { username, obj };
  },
};
```

### ref

- Provided for reactive code by vue
- Used to wrap nuber, string, objects etc
- Values are accesssed in java using `objName.value`, in html thn can be accessed directly objName

### reactive

- Made specficially for objects
- A wrapper class, but we dont need to access to using `.value`
- Can be accessed directly
- Basically allow reactivity without wrappers such as `.value`
