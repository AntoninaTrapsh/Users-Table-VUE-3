<template>
  <user-information></user-information>
</template>

<script>

import UserInformation from "@/pages/user_information";

export default {
  name: 'App',
  components: {UserInformation},
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}
</style>
