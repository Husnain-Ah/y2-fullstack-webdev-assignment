<template>
  <div>
    <nav class ="navbar navbar-light bg-primary">
      <router-link class="navbar-brand text-light" to="/">Home </router-link>
      <br />
      <router-link class="navbar-brand text-light" to="/login">Login</router-link>
      <br />
    </nav>
    <router-view />
  </div>
</template>