<template>
  <div class="dropper">
    <input
      type="file"
      @change="uploadImages($event.target.files)"
      multiple
      accept="image/*"
    />
    <span>Drag files here!</span>
  </div>
</template>

<script>
import api from '../api/imgur';

export default {
  name: 'UploadForm',
  methods: {
     uploadImages: function(images) {
      // Get the access token
      const { token } = window.localStorage.getItem('imgur_token');

      // Call our API module to do the upload
      api.uploadImages(images, token).then(function() {
        // Redirect our user to ImageList component
        window.location.hash = '/'
      })
  
    }
  },
  computed: {
    isLoggedIn() {
      return !!this.token
    },
    token() {
      return window.localStorage.getItem('imgur_token')
    }
  },
};
</script>

<style scoped>
.dropper {
  height: 30vh;
  border: 2px dashed black;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.dropper:hover {
  background-color: #eee;
}
input {
  width: 100%;
  height: 30vh;
  position: absolute;
  opacity: 0;
}
</style>
