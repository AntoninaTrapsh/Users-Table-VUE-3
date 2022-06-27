<template>
  <input class='form-input' :value='modelValue' @input='updateInput'/>
</template>

<script>
export default {
  name: 'form-input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(event) {
      this.$emit('update:modelValue', event.target.value)
    },

  }
}
</script>

<style scoped>
.form-input {
  border: none;
  outline: none;
  border-bottom: 1px solid teal;
  font-size: 1em;
  padding: 5px 0;
  margin: 10px 0 5px 0;
  width: 100%;
}
</style>