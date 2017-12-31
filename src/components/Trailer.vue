<template>
  <div class="video-overlay" @click.self="closeVideo" :class="{ opened : opened === true }">
    <div class="video-wrapper" :class="{ opened : opened === true }">
      <button class="close-button" @click="closeVideo"><icon name="close"></icon></button>
      <button v-if="paused" class="play-pause" :class="{ paused : paused === true }" @click="togglePlay" ><icon name="play"></icon></button>
      <button v-else class="play-pause" @click="togglePlay" ><icon name="pause"></icon></button>
      <video id="movie-trailer" ref="movieTrailer" @click="togglePlay" autoplay>
        <source src="https://m.media-amazon.com/images/G/01/IMDb/design/a/2017/ptp/00128761-jumanji/video1.mp4" type="video/ogg">
        Your browser does not support the video tag.
      </video>
    </div>
  </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

export default {
  name: 'Trailer',
  components: {
    'Icon': Icon
  },
  data () {
    return {
      opened: false,
      paused: false
    }
  },
  methods: {
    closeVideo: function () {
      this.$refs.movieTrailer.pause()
      let self = this
      this.opened = false
      setTimeout(function () {
        self.$emit('closeVideo')
      }, 150)
    },
    togglePlay: function () {
      const video = this.$refs.movieTrailer
      if (video.paused) {
        video.play()
        this.paused = false
      } else {
        video.pause()
        this.paused = true
      }
    },
    animateIn: function () {
      let self = this
      setTimeout(function () {
        self.opened = true
      }, 50)
    }
  },
  mounted () {
    this.animateIn()
  }
}
</script>

<style lang="scss" scoped>
  @mixin transition($transition...) {
    -moz-transition:    $transition;
    -o-transition:      $transition;
    -webkit-transition: $transition;
    transition:         $transition;
  }

  @mixin transform($transform...) {
    -moz-transform: $transform;
    -o-transform: $transform;
    -webkit-transform: $transform;
    transform: $transform;
  }

  .video-overlay {
    position: fixed;
    z-index: 4;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0);
    @include transition(all 0.1s linear);

    &.opened {
      background-color: rgba(0, 0, 0, 0.8);
      @include transition(all 0.3s linear);
    }

    .video-wrapper {
      width: 10%;
      max-width: 1200px;
      position: absolute;
      z-index: 5;
      top: 50%;
      left: 50%;
      @include transform(translateX(-50%) translateY(-50%));
      @include transition(all 0.1s linear);

      &.opened {
        width: 80%;
        @include transition(all 0.3s linear);
      }

      .close-button {
        opacity: 0;
        position: absolute;
        z-index: 5;
        top: 5px;
        right: 5px;
        background-color: rgba(0, 0, 0, 0.1);
        border: 2px solid rgba(255, 255, 255, 0.6);
        border-radius: 50%;
        color: rgba(255, 255, 255, 0.6);
        font-size: 20px;
        text-transform: uppercase;
        width: 50px;
        height: 50px;
        cursor: pointer;
        @include transition(all 0.2s linear);

        &:hover {
          background-color: rgba(255, 255, 255, 0.2);
        }

        &:focus {
          outline: none;
        }
      }

      .play-pause {
        opacity: 0;
        position: absolute;
        border: 2px solid rgba(255, 255, 255, 0.4);
        border-radius: 50%;
        height: 100px;
        width: 100px;
        background-color: rgba(0, 0, 0, 0.5);
        z-index: 6;
        top: 50%;
        left: 50%;
        cursor: pointer;
        @include transform(translateX(-50%) translateY(-50%));
        @include transition(opacity 0.2s linear);

        &.paused {
          padding-left: 18px;
        }

        &:focus {
          outline: none;
        }

        .fa-icon {
          color: rgba(255, 255, 255, 0.4);
          width: 50px;
          height: 50px;
        }
      }

      video {
        width: 100%;
        cursor: pointer;
      }

      &:hover {
        .play-pause {
          opacity: 1;
        }
        .close-button {
          opacity: 1;
        }
      }
    }
  }
</style>