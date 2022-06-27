<template>
  <div class='users'>
    <h1 class='users__title'>Таблица пользователей</h1>
    <create-button class='users__btn' @click='isModalVisible = true'>Добавить нового пользователя</create-button>
    <modal-window class='users__modal' v-model:isShow='isModalVisible'>
      <form-creation :options='headList' class='users__form' @create='addUser'></form-creation>
    </modal-window>
    <user-table class='users__table' @create='sortUser' :users='users'></user-table>
    <div class='users__warning' v-if='!this.users.length'>
      <strong>Таблица пуста.</strong> <p>Добавьте первого пользователя</p>
    </div>
  </div>
</template>

<script>
import FormCreation from '@/components/form_creation';
import UserTable from '@/components/user_table';

export default {
  name: 'user-information',
  components: {FormCreation, UserTable},
  data() {
    return {
      users: [],
      headList: [],
      isModalVisible: false,
      sortKey: null
    }
  },
  methods: {
    addUser(user) {
      if (user.head) {
        const head = this.searchUser(this.users, user.head)
        head.subordinate.push(user);

        this.sortTable(head.subordinate, this.sortKey);

      } else {
        this.users.push(user);
      }
      this.headList.push(user);
      this.isModalVisible = false;
    },
    loadUsers() {
      const savedUsers = (JSON.parse(localStorage.getItem('users')));
      const savedHeads = (JSON.parse(localStorage.getItem('head-list')));
      this.users.push(...savedUsers);
      this.headList.push(...savedHeads);
    },
    searchUser(userList, id) {
      const stack = [...userList];
      while (stack.length) {
        const user = stack.pop();
        if (user.id === +id) {
          return user;
        } else {
          if (user.subordinate) {
            stack.push(...user.subordinate);
          }
        }
      }
    },
    sortTable(users, sortKey) {
        return users.sort((user1, user2) => {
          if (user1[sortKey] > user2[sortKey]) {
            return 1;
          }
          if (user1[sortKey] < user2[sortKey]) {
            return -1;
          }
          return 0;

        });
    },
    sortUser(sortCondition) {
      const sortKey = sortCondition === 'Имя' ? 'name' : 'phone';
      if (this.sortKey === sortKey) {
        return;
      }

      this.sortKey = sortKey;

      const stack = [...this.users];
      while (stack.length) {
        const user = stack.pop();
          if (user.subordinate?.length) {
            stack.push(...this.sortTable(user.subordinate, sortKey));
          }
      }

      this.sortTable(this.users, sortKey);
    },
    beforeWindowUnload() {
        localStorage.setItem('users', JSON.stringify(this.users));
        localStorage.setItem('head-list', JSON.stringify(this.headList));
    },
  },
  created() {
    window.addEventListener('beforeunload', this.beforeWindowUnload)
  },
  mounted() {
    this.loadUsers();
  },
  beforeUnmount() {
    window.removeEventListener('beforeunload', this.beforeWindowUnload)
  },
}
</script>

<style scoped>
.users {
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.users__warning {
  margin-top: 20px;
  width: 400px;
  text-align: center;
}

.users__btn {
  margin: 15px 0;
}
</style>