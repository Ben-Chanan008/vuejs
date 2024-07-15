<script setup>
  import { defineProps } from 'vue';

  defineProps({
    bg: {
      type: String,
      default: 'bg-gray-100'
    },
    className: {
      type: String,
      default: 'bg-gray-300'
    }
  });
</script>

<template>
  <div :class="`${bg} p-6 rounded-lg shadow-md`">
    <slot></slot> `
  </div>
</template>


<style scoped>

</style>
