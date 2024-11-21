<template>
  <q-date
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: String, // Date value in YYYY-MM-DD format
    props: Object, // Additional props for q-date
  },
  emits: ['update:modelValue'], // Emit v-model updates
  methods: {
    updateValue(value) {
      this.$emit('update:modelValue', value); // Emit the updated date
    },
  },
};
</script>
