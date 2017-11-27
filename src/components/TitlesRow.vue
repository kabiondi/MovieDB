<template>
  <div class="titles-row">
    <div class="title-category">{{ categoryName }}</div>
    <div class="carousel">
      <ul :style="{ left: _left + 'vw'}">
        <template v-for="title in titles">
          <li>
            <div class="image-div">
              <img :src="title.poster" />
            </div>
            <div class="details">
              <div>{{ title.rating }}</div>
              <div>{{ title.genres }}</div>
              <div>{{ title.title }}</div>
            </div>
          </li>
        </template>
      </ul>
      <div class="titles-left" @click="titlesPosition -= 1">
        <icon name="chevron-left"></icon>
      </div>
      <div class="titles-right" @click="titlesPosition += 1">
        <icon name="chevron-right"></icon>
      </div>
    </div>
   </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

export default {
  name: 'TitlesRow',
  components: {
    'Icon': Icon
  },
  props: [
    'categoryName',
    'titles'
  ],
  data () {
    return {
      titlesPosition: 0
    }
  },
  // methods: {
  //   titlesRight: function () {
  //     alert('hello')
  //   }
  // },
  computed: {
    _left: function () {
      return -88.5 * this.titlesPosition
    }
  }
}
</script>

<style lang="scss" scoped>
// variables
$large: "(min-width: 1250px)";
$x-large: "(min-width: 1500px)";

@mixin transform($transform...) {
  -moz-transform: $transform;
  -o-transform: $transform;
  -webkit-transform: $transform;
  transform: $transform;
}

.titles-row {
  font-size: 20px;
}
.title-category {
  padding: 0.2em 2%;
  margin: 0.4%;
  font-size: 1.2em;
  text-align: left;
}
.carousel {
  position: relative;
  ul {
    //padding: 0 2%;
    //margin: 0 0 1.5em;
    padding: 0;
    margin: 0 5vw;
    //display: flex;
    //width: 196%;
    white-space: nowrap;
    position: relative;
    @media #{$large} {
      width: 172%;
    }
    @media #{$x-large} {
      width: 147%;
    }
    li {
      display: inline-block;
      width: 16.9vw;
      box-shadow: 0 0 10px 2px rgba(0,0,0,0.3), 0 0 10px 2px rgba(0,0,0,0.1);
      max-width: 220px;
      margin: 0 0.4vw;
      cursor: pointer;
      .image-div {
        img {
          width: 100%;
          height: 100%;
          display: flex;
        }
      }
      .details {
        font-size: 0.8em;
        padding: 0.5em;
        height: 4em;
        background-color: #fff;
      }
    }
  }
  .titles-right,
  .titles-left {
    position: absolute;
    top: 0;
    bottom: 0;
    background-color: #ccc;
    opacity: 0.3;
    cursor: pointer;
    color: #777;
    .fa-icon {
      position: absolute;
      top: 50%;
      left: 50%;
      @include transform(translateY(-50%) translateX(-50%));
      width: auto;
      height: 15%;
      max-width: 100%;
      max-height: 100%;
    }
    &:hover {
      opacity: 0.8;
      background-color: #333;
      color: #555;
    }
  }
  .titles-left {
    width: 4.6vw;
    left: 0;
  }
  .titles-right {
    width: 6.2vw;
    left: 93.8vw;
  }
}
</style>



