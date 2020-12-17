<template>
  <v-form v-model="valid">
    <v-text-field
      v-if="hasName"
      v-model="userInfo.name"
      label="Name"
      required
    />
    <v-text-field v-model="userInfo.email" label="Email" required />
    <v-text-field
      v-model="userInfo.password"
      label="Password"
      :type="showPassword ? 'text' : 'password'"
      :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
      counters="true"
      @click:append="showPassword = !showPassword"
    />
    <v-btn :disabled="!valid" @click="submitForm(userInfo)">{{
      buttonText
    }}</v-btn>
  </v-form>
</template>

<script>
export default {
  props: ['submitForm', 'buttonText', 'hasName'],
  data() {
    return {
      valid: false,
      showPassword: false,
      userInfo: {
        email: 'imalsha@gmail.com',
        password: '12345',
      },
    }
  },
}
</script>

<style lang="scss" scoped></style>
