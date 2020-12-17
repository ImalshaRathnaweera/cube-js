<template>
  <v-container>
    <h1>Registration</h1>
    <UserAuthForm
      button-text="Register"
      :submit-form="registerUser"
      has-name="true"
    />
  </v-container>
</template>

<script>
import UserAuthForm from '@/components/UserAuthForm'
export default {
  components: {
    UserAuthForm,
  },
  methods: {
    registerUser(registrationinfo) {
      alert('regitration successful')
    },
  },
}
</script>

<style lang="scss" scoped></style>
