<!-- NOTE: the modelValue property is the default name of the property that Vue will look for when double binding through v-model to custom components-->
<!-- Also, onChange event listener is not a direct binding unlike @change keyword used in BaseInput -->
<!-- If we choose not to use the @ sing syntax, the event will be prefixed by the keyword on, in this case onChange since were listening to the change event -->
<template>
  <label v-if="label">{{ label }}</label>
  <select
    :value="modelValue" 
    class="field"
    v-bind="{
      ...$attrs,
      onChange: ($event) => { $emit('update:modelValue', $event.target.value)}
    }"
  >
    <option
      v-for="option in options"
      :value="option"
      :key="option"
      :selected="option === modelValue"
    >{{ option }}</option>
  </select>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    modelValue: {
      type: [String, Number],
      default: ''
    },
    options: {
      type: Array,
      required: true
    }
  }
}
</script>