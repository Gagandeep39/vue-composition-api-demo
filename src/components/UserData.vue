<template>
  <div>
    <h2>{{ userName }}</h2>
    <h3>{{ age }}</h3>
    <h3>{{ lastName }}</h3>
  </div>
</template>
<script>
import { computed, inject } from 'vue';
export default {
  props: ['userName', 'age'],
  setup(props, context) {
    const combination = computed(() => props.userName + ' ' + props.age);

    // Context allows access to slots data, eit events
    console.log(context);

    // ########## Inject ###########
    const lastName = inject('lastName');
    console.log(lastName);
    return {
      combination,
      lastName,
    };
  },
};
</script>
<style lang=""></style>
