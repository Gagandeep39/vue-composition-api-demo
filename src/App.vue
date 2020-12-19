<template>
  <div>
    <p>{{ username }}</p>
    <p>{{ obj.name }}</p>
  </div>
</template>

<script>
import { ref } from 'vue';

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
