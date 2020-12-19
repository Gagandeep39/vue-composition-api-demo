# Vue Composition API

- [Vue Composition API](#vue-composition-api)
  - [Deployment](#deployment)
  - [Description](#description)
  - [Composition API Details](#composition-api-details)
  - [Demo](#demo)
    - [ref](#ref)
    - [reactive](#reactive)
  - [Methods](#methods)
  - [Computed](#computed)
  - [2 way binding](#2-way-binding)
  - [Watch](#watch)
  - [Ref](#ref-1)

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

## Methods

- Same as writing functions in react and other javascript frameworks

```js
setup() {
  // Function in Composition API
  const showAlert = () => {
    alert('This is an alert');
  };
  return { showAlert };
},
```

## Computed

- Called when variable inside it changes
- Created as a method

```html
<input type="text" @input="setFirstName" />
<input type="text" @input="setLastName" />
<p>{{ fullName }}</p>
```

```js
import { ref, computed } from 'vue';

export default {
  setup() {
    // ############# Computed properties #############
    let firstName = ref('');
    let lastName = ref('');
    function setFirstName(event) {
      firstName.value = event.target.value;
    }
    function setLastName(event) {
      lastName.value = event.target.value;
    }
    // Computed method
    const fullName = computed(() => firstName.value + ' ' + lastName.value);
    return {
      firstName,
      lastName,
      setFirstName,
      setLastName,
      fullName,
    };
  },
};
```

## 2 way binding

```html
<input type="text" v-model="description" placeholder="Description" />
{{description }}
```

```js
const description = ref('');
```

## Watch

- Execut a method if a value change

```js
import { ref, watch } from 'vue';

export default {
  setup() {
    let firstName = ref('');
    let lastName = ref('');
    // ################ Watchers ################
    // Watch single value
    watch(firstName, (newVal, oldVal) => {
      console.log('First name was changed');
      console.log(newVal, oldVal);
    });
    watch([firstName, lastName], (newVal, oldVal) => {
      console.log('first name and last name changed');
      console.log(newVal, oldVal); // newvalue - Array of parameters being atched, oldval - arra of param being watch
    });

    return {
      firstName,
      lastName,
    };
  },
};
```

## Ref

- We dont have access to this.\$ref
- Instead we creat a variable as `const abc = ref(null)` and expose it

```html
<input type="text" ref="ageInput" /> <button @click="setAge">Set age</button>
```

```js
import { ref } from 'vue';

export default {
  setup() {
    // ################Age ################
    const ageInput = ref(null);
    const age = ref(22);
    function setAge() {
      // .value is Twice because, when we use ref, we access the data using .value in options API,
      // IN comosition API reference requires its own .value
      age.value = ageInput.value.value;
      console.log(age.value);
    }
    return {
      setAge,
      ageInput,
    };
  },
};
```
