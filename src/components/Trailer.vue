<template>
  <div class="video-container">
    <button class="close-button" @click="closeVideo">Close</button>
    <video id="movie-trailer" ref="movieTrailer" controls autoplay>
      <source src="https://m.media-amazon.com/images/G/01/IMDb/design/a/2017/ptp/00128761-jumanji/video1.mp4" type="video/ogg">
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<script>
export default {
  name: 'Trailer',
  methods: {
    closeVideo: function () {
      this.$emit('closeVideo')
    }
  }
}
</script>

<style lang="scss" scoped>
  .close-button {
    background-color: red;
    width: 100px;
    height: 50px;
  }
  video {
    position: absolute;
    top: 0;
    z-index: 4;
  }
</style>