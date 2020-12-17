<template>
  <v-app>
    <v-app-bar app color="#00796B" height="80px">
      <h1>Cube JS Dashboard App</h1>
      <v-spacer />

      <div v-if="$auth.loggedIn">
        {{ $auth.user.email }}
        <v-btn text>Logout</v-btn>
      </div>
      <div v-else>
        <v-btn text to="/login">Login</v-btn>
        <v-btn text to="/register">Register</v-btn>
      </div>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
  </v-app>
</template>

<script>
export default {}
</script>

<style scoped></style>
