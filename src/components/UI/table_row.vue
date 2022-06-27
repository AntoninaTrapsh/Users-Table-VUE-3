<template>
  <tr class='user-line'>
    <td class='user-line__name'>
      <create-button class='user-line__btn' v-if='user.subordinate && user.subordinate.length'
                     @click='expandSubordinates' style='padding: 2px 2px'>
        {{openingSign}}
      </create-button>
      {{user.name}}
    </td>
    <td class='user-line__phone'>{{user.phone}}</td>
  </tr>
  <tbody class='user-line__subordinates' v-show='isShowSubordinate' v-for='u in user.subordinate' :key='u.id'>
    <table-row :user='u'></table-row>
  </tbody>
</template>

<script>
export default {
  name: 'table-row',
  data() {
    return {
      isShowSubordinate: false,
      openingSign: '+'
    }
  },
  props: {
    user: {
      type: Object
    },
  },
  methods: {
    expandSubordinates() {
      this.isShowSubordinate = !this.isShowSubordinate;
      this.openingSign = this.isShowSubordinate ? '-' : '+';
    }
  }
}
</script>

<style scoped>
.user-line__name, .user-line__phone {
  background: white;
  padding: 5px;
  border: 1px solid teal;
  width: 200px;
  text-align: left;
}

.user-line__subordinates {
  border-collapse: collapse;
  display: block;
  margin-left: 2%;
}

.user-line {
  display: flex;
}
</style>

