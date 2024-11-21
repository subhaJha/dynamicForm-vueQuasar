<template>
  <q-input
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
    type="textarea"
  />
</template>

<script>
export default {
  props: {
    modelValue: String, // Value for textarea
    props: Object, // Additional props for q-input
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated value
    },
  },
};
</script>
