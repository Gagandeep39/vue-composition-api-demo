<template>
  <div>
    <h2>Check Code / Logs for more info</h2>
    <p>This is a demo application for understanding reativity</p>
    <p>{{ username }}</p>
    <p>{{ obj.name }}</p>
    <input type="text" @input="setFirstName" />
    <input type="text" @input="setLastName" />
    <p>{{ fullName }}</p>
    <button @click="showAlert">Show alert</button>
  </div>
</template>

<script>
import { isReactive, isRef, reactive, ref, toRefs, computed } from 'vue';

export default {
  setup() {
    // Refs
    const username = ref('Gagandeep');
    const obj = ref({ name: 'Gagan', age: 21 });
    // ###############  Ref  ################
    // Accessing object
    console.log(obj);
    console.log(obj.value.name);
    // Checkiing if it is reactive
    console.log(isRef(obj)); // True
    console.log(isRef(obj.value.name)); // False
    // ###############  Reactive  ###############
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

    // ############## Function #############
    const showAlert = () => {
      alert('This is an alert');
    };

    // ############# Computed properties #############
    let firstName = ref('');
    let lastName = ref('');
    function setFirstName(event) {
      firstName.value = event.target.value;
    }
    function setLastName(event) {
      lastName.value = event.target.value;
    }
    const fullName = computed(() => firstName.value + ' ' + lastName.value);
    return {
      username,
      obj,
      showAlert,
      firstName,
      lastName,
      setFirstName,
      setLastName,
      fullName,
    };
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
