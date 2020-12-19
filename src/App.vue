<template>
  <div>
    <h2>Check Code / Logs for more info</h2>
    <p>This is a demo application for understanding reativity</p>
    <p>{{ username }}</p>
    <p>{{ obj.name }}</p>
  </div>
</template>

<script>
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
    // Making child reactive
    const refObj = toRefs(obj2);
    console.log(isRef(refObj.name));
    return { username, obj };
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
