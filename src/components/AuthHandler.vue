<template>
  <div>
    Please wait...
  </div>
</template>

<script>
import qs from 'qs';

export default {
  name: 'AuthHandler',
  methods:  {
    finalizeLogin( hash) {
      const query = qs.parse(hash.replace('#', ''));
      window.localStorage.setItem('imgur_token', query.access_token);
      window.location.pathname = '/';
    }
  },
  created() {
    this.finalizeLogin(window.location.hash);
  }
};
</script>
