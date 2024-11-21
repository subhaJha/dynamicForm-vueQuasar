<template>
  <q-input
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: [String, Number], // Prop for v-model
    props: Object, // Additional props for q-input
  },
  emits: ['update:modelValue'], // Declare the emit for v-model
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit updated value to parent
    },
  },
};
</script>
