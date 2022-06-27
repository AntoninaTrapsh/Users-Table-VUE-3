<template>
  <form class='create-form' @submit.prevent>
    <form-input class='create-form__name' v-model="name" type='text' placeholder='Введите имя' @blur='v$.name.$touch'/>
    <div v-if='v$.name.$error' class='create-form__warning'>Это поле обязательное</div>
    <form-input class='create-form__phone' v-model='phone' type='number' placeholder='Введите номер телефона' @blur='v$.phone.$touch'/>
    <div v-if='v$.phone.$error' class='create-form__warning'>Это поле обязательное</div>
    <head-select class='create-form__select' :options='options' v-model='selectHead'></head-select>
    <create-button class='create-form__btn' type='submit'
                   @click='addUser' :disabled='v$.$invalid'>Создать</create-button>
  </form>
</template>

<script>
import useVuelidate from '@vuelidate/core';
import { required, numeric } from '@vuelidate/validators';
export default {
  name: 'form-creation',
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  setup () {
    return { v$: useVuelidate() }
  },
  data() {
    return {
      id: Date.now(),
      user: {},
      name: null,
      phone: null,
      selectHead: null,
    }
  },
  validations() {
    return {
      name: { required, $lazy: true },
      phone: { required, $lazy: true, numeric }
    }
  },
  methods: {
    addUser() {
      this.v$.$validate()
      if (this.v$.$error) {
        alert('Введите данные о пользователе');
        return;
      }
      [this.user.name, this.user.phone, this.user.id, this.user.head] =
          [this.name, this.phone, Date.now(), this.selectedHead];
      this.user.subordinate = [];
      this.$emit('create', this.user);
      this.user = {
        name: null,
        phone: null
      }
    },
  },
  watch: {
    selectHead(selectedHead) {
      this.selectedHead = selectedHead;
    }
  }
}
</script>

<style scoped>
.create-form {
  display: flex;
  flex-direction: column;
}
.create-form__name, .create-form__phone {
  margin-top: 15px;
}
.create-form__select {
  margin: 15px 0;
}
.create-form__btn {
  align-self: flex-end; margin-top: 15px
}
.create-form__warning {
  color: #ea7e7e;
  font-size: 12px;
}
</style>