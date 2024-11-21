<template>
  <q-expansion-item
    v-bind="props"
    :expanded="localExpanded"
    @update:expanded="updateExpanded"
    expand-separator
  >
    <!-- Correctly define the header slot -->
    <template #header>
      <div class="header">
        <span class="accordion-header">{{ props?.label || 'Accordion' }}</span>
      </div>
    </template>
    <slot />
  </q-expansion-item>
</template>

<script>
export default {
  props: {
    expanded: Boolean,
    props: {
      type: Object,
      default: () => ({}),
    },
  },
  emits: ['update:expanded'],
  data() {
    return {
      localExpanded: this.expanded,
    };
  },
  watch: {
    expanded(newVal) {
      this.localExpanded = newVal;
    },
  },
  methods: {
    updateExpanded(value) {
      this.localExpanded = value;
      this.$emit('update:expanded', value);
    },
  },
};
</script>

<style scoped>
/* .q-expansion-item, */
/* .q-item-type, */
/* .q-expansion-item--collapsed, */
.q-focus-helper {
  background-color: #808080 !important;
  font-weight: bold;
  font-size: 16px;
}
</style>
