<template>
  <q-rating
    v-bind="props"
    :model-value="modelValue"
    @update:model-value="updateValue"
  />
</template>

<script>
export default {
  props: {
    modelValue: {
      type: Number, // Rating value is typically a number
      required: true,
    },
    props: {
      type: Object,
      default: () => ({}), // Additional props for QRating
    },
  },
  emits: ['update:modelValue'],
  methods: {
    updateValue(value) {
      // console.log('RatingField emitting value:', value); // Debug log
      this.$emit('update:modelValue', value); // Emit value to parent
    },
  },
};
</script>
