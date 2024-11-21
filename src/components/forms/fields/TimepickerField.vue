<template>
  <q-time
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: String, // Time value in HH:mm or HH:mm:ss format
    props: Object, // Additional props for q-time
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated time
    },
  },
};
</script>
