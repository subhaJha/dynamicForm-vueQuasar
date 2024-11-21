<template>
  <q-slider
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: [Number, Array], // Single value or range for slider
    props: Object, // Additional props for q-slider
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated value
    },
  },
};
</script>
