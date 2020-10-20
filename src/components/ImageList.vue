<template>
  <div>
    <div v-if="isLoggedIn" class="image-container">
      <img :alt="image.title" :key="image.link" v-for="image in allImages" :src="image.link"  />
    </div>
    <h2 v-else>Log in to get started!</h2>
  </div>
</template>

<script>
import api from '../api/imgur'

export default {
  data: () => ({
    allImages: []
  }),
  name: 'ImageList',
  computed: {
    isLoggedIn: () => !!window.localStorage.getItem('imgur_token')
  },
  methods: {
    fetchImages() {
      const token = window.localStorage.getItem('imgur_token')
      const instance = this;
      api.fetchImages(token).then(response => instance.allImages = response.data.data)
    }
  },
  created() {
    this.fetchImages();
  }
};
</script>

<style scoped>
.image-container {
  column-count: 3;
  column-gap: 0;
}
img {
  max-width: 100%;
  padding: 5px;
}
</style>
