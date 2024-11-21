<template>
  <q-radio
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: [String, Number], // Value for the selected radio
    props: Object, // Additional props for q-radio
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated value
    },
  },
};
</script>
