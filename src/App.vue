<script setup>

</script>

<template>
  <div class="centered-div">
    <h1 class="centered">Welcome to VIEIRA BJJ</h1>
    <h3 class="centered">(brazilian Jiu jitsu)</h3>
    <p class="centered">login/register bellow.</p>

    <div v-if="isLoggedIn">
        <h2>Hello {{ userName }}</h2>
        <button @click="handleLogout">Log Out</button>
    </div>
    <div v-else class="centered">
        <GoogleLogin :callback="callback" />
        <hr>
        <button><RouterLink to="/">Guest LogIn</RouterLink></button>
    </div>
  </div>

  <RouterView />  

</template>

<style>

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
  background-color: rgb(238, 237, 237);
}
.centered-div {
  width: 500px;
  height: 500px;
  background-color: rgb(255, 255, 255);
}
.centered {
  text-align: center;
}
button {
  font-size: 30px;
  text-decoration: none;
}
</style>
