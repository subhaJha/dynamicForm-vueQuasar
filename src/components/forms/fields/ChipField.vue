<template>
  <q-chip
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: [String, Array], // Single or multiple chips
    props: Object, // Additional props for q-chip
  },
  emits: ['update:modelValue'],
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value);
    },
  },
};
</script>
