<template>
  <div>
    <h1 class="q-mb-lg">Dynamic Form Example</h1>
    <DynamicForm
      :fields="formFields"
      v-model="formValues"
      :expanded-state="expandedState"
      @update:modelValue="onModelValueUpdate"
      @update:expandedState="onExpandedStateUpdate"
    />

    <q-btn
      label="Submit"
      color="primary"
      class="q-mt-md"
      @click="handleFormSubmit"
    />
  </div>
</template>

<script>
import { reactive, watch } from 'vue';
import DynamicForm from 'src/components/forms/DynamicForm.vue';
import formFieldsJson from 'src/assets/formFields.json';

export default {
  components: {
    DynamicForm,
  },
  setup() {
    const formFields = reactive(formFieldsJson.fields);

    // Initialize formValues
    const initializeFormValues = (fields) => {
      const values = {};
      Object.keys(fields).forEach((key) => {
        values[key] = fields[key].children
          ? initializeFormValues(fields[key].children)
          : '';
      });
      return values;
    };

    const formValues = reactive(initializeFormValues(formFields));

    // Manage expanded states for each accordion
    const initializeExpandedStates = (fields) => {
      const states = {};
      Object.keys(fields).forEach((key) => {
        states[key] = false; // Default: collapsed
      });
      return states;
    };

    const expandedState = reactive(initializeExpandedStates(formFields));

    watch(
      formValues,
      (newValues) => {
        console.log(
          'Parent FormPage: formValues updated:',
          JSON.stringify(newValues, null, 2)
        );
      },
      { deep: true }
    );

    const onModelValueUpdate = (newValues) => {
      Object.assign(formValues, newValues); // Update parent state
    };
    const onExpandedStateUpdate = ({ key, value }) => {
      expandedState[key] = value; // Update the expanded state
    };
    const handleFormSubmit = () => {
      console.log(
        'Final Submitted Values:',
        JSON.stringify(formValues, null, 2)
      );
      alert(`Submitted Values:\n${JSON.stringify(formValues, null, 2)}`);
    };

    return {
      formFields,
      formValues,
      expandedState,
      onModelValueUpdate,
      handleFormSubmit,
      onExpandedStateUpdate,
    };
  },
};
</script>
