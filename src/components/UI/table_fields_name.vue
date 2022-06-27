<template>
  <tr>
    <th @click="$emit('create', fieldsName.firstField)">{{fieldsName.firstField}}</th>
    <th @click="$emit('create', fieldsName.secondField)">{{fieldsName.secondField}}</th>
  </tr>
</template>

<script>
export default {
  name: 'table-fields-name',
  props: {
    fieldsName: {
      type: Object
    },
  }
}
</script>

<style scoped>
th {
  width: 200px;
  background: white;
  padding: 5px;
  border: 1px solid teal;
}
</style>