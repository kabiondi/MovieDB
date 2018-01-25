<template>
  <div class="titles-row">
    <div class="title-category">{{ category.name }}</div>
    <div class="carousel">
      <ul :style="{ left: _left + 'vw'}">
        <template v-for="title in titleData">
          <li>
            <div class="image-div">
              <div class="list-add" @click="toggleMyList(title.title)"><span>My List</span><icon name="plus-circle"></icon></div>
              <div class="play">
                <icon name="play-circle-o"></icon>
              </div>
              <img :src="title.poster" />
            </div>
            <div class="details">
              <div class="rating">
                <span>
                  <icon name="star"></icon>
                </span>
                {{ title.rating }}
              </div>
              <div class="rated">{{ title.rated }}</div>
              <div class="title">{{ title.title }}</div>
              <div class="genres">{{ title.genres }}</div>
            </div>
          </li>
        </template>
        <li v-for="slide in _blankSlidesCount" class="blank-tile"></li>
      </ul>
      <div v-show="titlesPosition > 0" class="titles-left" @click="titlesLeft">
        <icon name="chevron-left"></icon>
      </div>
      <div v-show="_titlesRight > 0" class="titles-right" @click="titlesRight">
        <icon name="chevron-right"></icon>
      </div>
    </div>
   </div>
</template>

<script>
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

const imdb = require('imdb-api')

export default {
  name: 'TitlesRow',
  components: {
    'Icon': Icon
  },
  props: [
    'category'
  ],
  data () {
    return {
      titleData: [],
      titlesPosition: 0,
      columns: 0
    }
  },
  computed: {
    _titlesCount () {
      return Object.keys(this.titleData).length
    },
    _titlesRight () {
      return this._titlesCount - this.titlesPosition - this.columns
    },
    _left: function () {
      return -88.5 * this.titlesPosition / this.columns
    },
    _blankSlidesCount () {
      return Math.max(0, this.columns - this._titlesCount)
    }
  },
  methods: {
    titlesLeft: function () {
      if (this.titlesPosition >= this.columns) {
        this.titlesPosition -= this.columns
      } else {
        this.titlesPosition -= this.titlesPosition
      }
    },
    titlesRight: function () {
      if (this._titlesRight >= this.columns) {
        this.titlesPosition += this.columns
      } else {
        this.titlesPosition += this._titlesRight
      }
    },
    getTitles: function () {
      const self = this
      this.category.titles.forEach(function (title) {
        imdb.get(title,
          // { apiKey: '4162605e',
          { apiKey: 'ac6f6f7b',
            timeout: 9000
          }).then(function (response) {
            self.titleData.push(response)
          })
        .catch(console.log)
      })
    },
    calcColumns: function (event) {
      let self = this
      let width = document.documentElement.clientWidth
      if (width > 1250) { self.columns = 6 } else
      if (width > 800) { self.columns = 5 } else
      if (width <= 800) { self.columns = 4 }

      if (typeof event === 'undefined') { return }
      if (event.type === 'resize' && this._titlesRight <= 0) {
        this.titlesPosition = this._titlesCount - this.columns
      }
    },
    toggleMyList: function (title) {
      this.$emit('addToMyList', title)
    }
  },
  created () {
    // this.getTitles()
    window.addEventListener('resize', this.calcColumns)
  },
  watch: {
    category: function () {
      this.titlesPosition = 0
      this.titleData = []
      this.getTitles()
    }
  },
  mounted () {
    this.getTitles()
    this.calcColumns()
  },
  destroyed () {
    window.removeEventListener('resize', this.calcColumns)
  }
}
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Roboto|Heebo|Yantramanav|Assistant|Montserrat:900');

// variables
$brand-red: #da3535;
$light-gold: #f3c532;
$gold: #e2b010;
$grey3: #333333;
$grey5: #555555;
$grey7: #777777;
$greyD: #dddddd;
$break-large: "1250px";
$break-small: "850px";

@mixin transform($transform...) {
  -moz-transform: $transform;
  -o-transform: $transform;
  -webkit-transform: $transform;
  transform: $transform;
}

@mixin transition($transition...) {
  -moz-transition:    $transition;
  -o-transition:      $transition;
  -webkit-transition: $transition;
  transition:         $transition;
}

.titles-row {
  font-family: 'Roboto';
  font-weight: 600;
  font-size: 20px;
  color: $grey7;
}
.title-category {
  padding: 0.2em 5vw;
  margin: 0.4%;
  font-size: 1.2em;
  text-align: left;
}
.carousel {
  position: relative;
  ul {
    padding: 0;
    margin: 0 5vw 3vw;
    white-space: nowrap;
    position: relative;
    @include transition(left 0.4s ease);
    li {
      display: inline-block;
      width: 16.9vw;
      box-shadow: 0 0 10px 2px rgba(0,0,0,0.3), 0 0 10px 2px rgba(0,0,0,0.1);
      max-width: 220px;
      margin: 0 0.4vw;
      cursor: pointer;
      @media screen and (min-width: $break-large) {
        width: 13.95vw;
      }
      @media screen and (max-width: $break-small) {
        width: 21.325vw;
      }
      @include transition(all, 0.2s)
      &.blank-tile {
        height: 31vw;
        background-color: transparent;
        @media screen and (min-width: $break-large) {
          height: 26vw;
        }
        @media screen and (max-width: $break-small) {
          height: 40vw;
        }
      }
      .list-add {
        opacity: 0;
        background-color: rgba(255, 255, 255, 0.9);
        position: absolute;
        top: 0;
        left: 0;
        color: $brand-red;
        font-size: 12px;
        padding: 0 5px 5px;
        box-shadow: 2px 2px 3px 1px rgba(0,0,0,0.2);
        border-bottom-right-radius: 5px;
        @include transition(all, 0.2s)
        span {
          //opacity: 0;
        }
        .fa-icon {
          margin-left: 6px;
          transform: translateY(26%);
        }
      }
      .image-div {
        position: relative;
        .play {
          position: absolute;
          opacity: 0;
          top: 50%;
          left: 50%;
          width: 50%;
          height: 50%;
          @include transform(translateX(-50%) translateY(-50%));
          @include transition(all, 0.2s)
          .fa-icon {
            color: #fff;
            width: 100%;
            height: 100%;
          }
        }
        img {
          width: 100%;
          height: 24.8vw;
          display: flex;
          @media screen and (min-width: $break-large) {
            height: 20.47vw;
          }
          @media screen and (max-width: $break-small) {
            height: 31.29vw;
          }
        }
      }
      .details {
        position: relative;
        font-family: 'Roboto';
        font-size: 0.75em;
        padding: 0.5em;
        height: 4.5em;
        background-color: #fff;
        font-weight: 600;
        div {
          white-space: nowrap;
          overflow: hidden;
          text-overflow: ellipsis;
        }
        .rating {
          margin-bottom: 0.3em;
        }
        .rated {
          position: absolute;
          top: 1em;
          right: 0.6em;
          color: $grey7;
          border: 1px solid #888;
          padding: 0 0.5em;
          font-size: 0.7em;
        }
        .title {
          font-family: 'Heebo';
          text-transform: uppercase;
          color: $grey7;
          margin-bottom: 0.2em;
        }
        .genres {
          font-family: 'Yantramanav';
          font-size: 0.9em;
          color: $gold;
        }
        .fa-icon {
          color: $light-gold;
          height: 1.1em;
          width: 1.1em;
          @include transform(translateY(12%))
        }
      }
      &:hover {
        box-shadow: 0 0 8px 4px rgba(0,0,0,0.5), 0 0 10px 2px rgba(0,0,0,0.1);
        .image-div {
          .play {
            opacity: 0.6;
          }
        }
        .list-add {
          opacity: 1;
        }
      }
    }
  }
  .titles-right,
  .titles-left {
    position: absolute;
    top: 0;
    bottom: 0;
    background-color: $grey5;
    opacity: 0.4;
    cursor: pointer;
    color: $greyD;
    @include transition(all 0.15s)
    .fa-icon {
      position: absolute;
      top: 50%;
      @include transform(translateY(-50%) translateX(-50%));
      width: auto;
      height: 15%;
      max-width: 100%;
      max-height: 100%;
    }
    &:hover {
      opacity: 0.8;
      background-color: #333;
    }
  }
  .titles-left {
    width: 4.6vw;
    left: 0;
    .fa-icon {
      left: 50%;
    }
  }
  .titles-right {
    width: 6.2vw;
    left: 93.8vw;
    .fa-icon {
      left: 40%;
    }
  }
}
</style>



