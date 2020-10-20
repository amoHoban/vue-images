<template>
  <div class="ui secondary pointing menu">
    <router-link to="/" class="active item">
      Image Storage
    </router-link>

    <div class="right menu">
      <div v-if="isLoggedIn" class="horizontal">
        <router-link to="/" class="item">Galleries</router-link>
        <router-link to="/upload" class="item">Upload</router-link>
        <a class="item" @click="logout">Logout</a>
      </div>

      <a v-else href="#" class="ui item" @click="login">
        Login
      </a>
    </div>
  </div>
</template>

<script>
import api from '../api/imgur'
export default {
  name: 'AppHeader',

  computed: {
    isLoggedIn: () => !!window.localStorage.getItem('imgur_token')
  },

  methods: {
    login: () => api.login(),

    logout: () => {
      window.localStorage.removeItem('imgur_token');
      window.location.pathname = '/';
    }
  }
};
</script>

<style scoped>
.horizontal {
  display: flex;
  flex-direction: row;
}
</style>
