<template>
  <q-card class="q-pa-md">
    <q-form>
      <div v-for="(field, key) in fields" :key="key" class="q-mb-md">
        <!-- Render component based on field type -->
        <component
          :is="resolveFieldComponent(field.type)"
          v-bind="field.props"
          v-model="formValues[key]"
          v-if="field.type !== 'q-accordion'"
          @update:modelValue="onFieldUpdate(key, $event)"
        />
        <!-- Handle Accordion Fields -->
        <AccordionField
          v-else
          :props="{ label: field.props.label }"
          :expanded="expandedState[key]"
          @update:expanded="onExpandedUpdate(key)"
          header-class="bg-primary text-white"
          expand-icon-class="text-white"
        >
          <DynamicForm
            :fields="field.children"
            v-model="formValues[key]"
            :expanded-state="expandedState[key]"
            @update:expandedState="$emit('update:expandedState', $event)"
          />
        </AccordionField>
      </div>
    </q-form>
  </q-card>
</template>

<script>
import { reactive, defineComponent, watch } from 'vue';
import TextField from './fields/TextField.vue';
import SelectField from './fields/SelectField.vue';
import CheckboxField from './fields/CheckboxField.vue';
import AccordionField from './fields/AccordionField.vue';
import RatingField from './fields/RatingField.vue';

export default defineComponent({
  props: {
    fields: {
      type: Object,
      required: true,
    },
    modelValue: {
      type: Object,
      required: true,
    },
    expandedState: {
      type: Object,
      required: true,
    },
  },
  components: {
    TextField,
    SelectField,
    CheckboxField,
    AccordionField,
    RatingField,
  },
  emits: ['update:modelValue', 'update:expandedState'],
  setup(props, { emit }) {
    // Recursive initialization of form values
    const initializeFormValues = (fields) => {
      const values = {};
      Object.keys(fields).forEach((key) => {
        if (fields[key].children) {
          values[key] = initializeFormValues(fields[key].children); // Recursive initialization for nested fields
        } else {
          values[key] = ''; // Default empty value for non-nested fields
        }
      });
      return values;
    };

    // Reactive local form values
    const formValues = reactive(initializeFormValues(props.fields));

    // Watch formValues for updates and emit changes to parent
    watch(
      formValues,
      (newValues) => {
        console.log('DynamicForm emitting update:modelValue:', newValues); // Debug log
        emit('update:modelValue', newValues);
      },
      { deep: true }
    );

    // Dynamically resolve field components
    const resolveFieldComponent = (type) => {
      switch (type) {
        case 'q-input':
          return 'TextField';
        case 'q-select':
          return 'SelectField';
        case 'q-checkbox':
          return 'CheckboxField';
        case 'q-accordion':
          return 'AccordionField';
        case 'q-rating':
          return RatingField;
        default:
          console.warn(`Unknown field type: ${type}`);
          return null;
      }
    };

    // Handle individual field updates
    const onFieldUpdate = (key, value) => {
      console.log(`Field [${key}] updated to:`, value);
      formValues[key] = value; // Sync updated value locally
    };

    // Handle expanded state updates
    const onExpandedUpdate = (key) => (value) => {
      emit('update:expandedState', { key, value });
    };

    return {
      formValues,
      resolveFieldComponent,
      onFieldUpdate,
      onExpandedUpdate,
    };
  },
});
</script>
