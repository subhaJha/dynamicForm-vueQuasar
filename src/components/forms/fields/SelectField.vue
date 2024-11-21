<template>
  <q-select
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
    emit-value
    map-options
  />
</template>

<script>
export default {
  props: {
    modelValue: [String, Number, Array], // Accepts single or multiple values
    props: {
      type: Object,
      default: () => ({}),
    },
  },
  emits: ['update:modelValue'], // Declare the emit event
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the new value to the parent
    },
  },
};
</script>
