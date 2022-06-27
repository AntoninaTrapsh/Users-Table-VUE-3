<template>
  <select class='head-select' @change='changeOptions'>
    <option class='head-select__option' value=''>Без начальства</option>
    <option class='head-select__option' v-for='option in options' :key='option.id' :value='option.id'>{{option.name + ' ' + option.phone}}</option>
  </select>
</template>

<script>

export default {
  name: 'head-select',
  props: {
    modelValue: {
      type: String
    },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOptions(event) {
      this.$emit('update:modelValue', event.target.value);
    }
  }
}
</script>

<style scoped>
select {
  height: 35px;
}
</style>