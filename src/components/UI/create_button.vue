<template>
  <button class='create-button'>
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'create-button'
}
</script>

<style scoped>
.create-button {
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

.create-button:hover {
  cursor: pointer;
  background: teal;
  color: white;
}

.create-button:disabled {
  background: #a2b0b0;
}

.create-button:disabled:hover {
  color: teal;
  cursor: default;
}
</style>