<template>
  <div>
    <h2>{{ userName }}</h2>
    <h3>{{ age }}</h3>
  </div>
</template>
<script>
import { computed } from 'vue';
export default {
  props: ['userName', 'age'],
  setup(props) {
    const combination = computed(() => props.userName + ' ' + props.age);
    return {
      combination,
    };
  },
};
</script>
<style lang=""></style>
