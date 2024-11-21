<template>
  <q-item-label v-bind="props" />
</template>

<script>
export default {
  props: {
    props: Object, // Props for q-item-label (e.g., text)
  },
};
</script>
