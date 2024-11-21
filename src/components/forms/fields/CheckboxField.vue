<template>
  <q-checkbox
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: Boolean, // Boolean prop for v-model
    props: Object, // Additional props for q-checkbox
  },
  emits: ['update:modelValue'], // Declare the emit for v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated value
    },
  },
};
</script>
