<template>
  <q-toggle
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: Boolean, // Value for toggle
    props: Object, // Additional props for q-toggle
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated value
    },
  },
};
</script>
