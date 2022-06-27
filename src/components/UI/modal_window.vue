<template>
  <div class='modal' v-if='isShow' @click='hideModal'>
    <div @click.stop class='modal__content'>
      <h3 class='modal__title'>Добавление пользователя</h3>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modal-window',
  props: {
    isShow: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideModal() {
      this.$emit('update:isShow', false)
    }
  }
}

</script>

<style scoped>
.modal {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0,0,0,0.5);
  position: fixed;
  display: flex;
}

.modal__content {
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300px;
  padding: 20px;
}
</style>