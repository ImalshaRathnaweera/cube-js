<template>
  <v-container>
    <h1>Login</h1>
    <UserAuthForm button-text="Login" :submit-form="loginUser" />
  </v-container>
</template>

<script>
import UserAuthForm from '@/components/UserAuthForm'

export default {
  components: {
    UserAuthForm,
  },
  methods: {
    loginUser(loginInfo) {
      // debugger
      this.$auth.loginWith('local', {
        data: loginInfo,
      })
      // alert('you pressed a button')
    },
  },
}
</script>

<style lang="scss" scoped></style>
