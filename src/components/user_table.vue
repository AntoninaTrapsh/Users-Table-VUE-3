<template>
  <table class='user-table'>
    <table-fields-name class='user-table__content' :fieldsName='fieldsName' @create='sortList'></table-fields-name>
    <tbody class='user-table__section' v-for='user in users' :key='user.id'>
    <table-row :user='user'></table-row>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'user-table',
  emits: ['create'],
  data() {
    return {
      fieldsName: {
        firstField: 'Имя', secondField: 'Телефон'
      },
    }
  },
  props: {
    users: {
      type: Array
    }
  },
  methods: {
    sortList(sortCondition) {
      this.$emit('create', sortCondition);
    }
  }
}
</script>

<style scoped>
.user-table {
  width: 400px;
  text-align: center;
  border-collapse: collapse;
  display: flex;
  flex-direction: column;
}
</style>