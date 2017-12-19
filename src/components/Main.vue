<template>
  <div class="app-container">
    <trailer v-if="showTrailer" @closeVideo="showTrailer = false"></trailer>
    <div class="hero">
      <div class="brand">MovieDb</div>
      <header class="menu">
        <ul>
          <li :class="{ active: activeHeroHeader === 'movies' }" @click="selectHeroHeader('movies')">Movies</li>
          <li :class="{ active: activeHeroHeader === 'photos' }" @click="selectHeroHeader('photos')">Photo Gallery</li>
          <li :class="{ active: activeHeroHeader === 'community' }" @click="selectHeroHeader('community')">Community</li>
          <li :class="{ active: activeHeroHeader === 'news' }" @click="selectHeroHeader('news')">News</li>
        </ul>
      </header>

      <div class="hero-details">
        <h1>Jumanji</h1>
        <ul>
          <li>Action</li>
          <li>Adventure</li>
          <li>Comedy</li>
        </ul>
        <div class="trailer-button" @click="playTrailer"><span>Watch Trailer</span><icon name="play-circle-o"></icon></div>
      </div>
      <img src="http://www.wallpapers4k.us/wp-content/uploads/2017/11/jumanji-welcome-to-the-jungle-wallpaper.jpg" />
      <div class="menu bottom">
        <div class="inner">
          <ul>
            <!-- <li :class="{ active: activeHeroSub === 'suggested' }" @click="selectHeroSub('suggested')">Suggested</li> -->
            <li :class="{ active: activeHeroSub === 'theaters' }" @click="selectHeroSub('theaters')">In Theaters</li>
            <li :class="{ active: activeHeroSub === 'coming' }" @click="selectHeroSub('coming')">Coming Soon</li>
            <li :class="{ active: activeHeroSub === 'mylist' }" @click="selectHeroSub('mylist')">My List</li>
            <li :class="{ active: activeHeroSub === 'suggested' }" @click="selectHeroSub('suggested')">Suggested</li>
            <!-- <li :class="{ active: activeHeroSub === 'tv' }" @click="selectHeroSub('tv')">TV Series</li> -->
            <!-- <li :class="{ active: activeHeroSub === 'trailers' }" @click="selectHeroSub('trailers')">Trailers</li> -->
            <li :class="{ active: activeHeroSub === 'more' }" @click="selectHeroSub('more')">More</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="titles">
      <div class="titles-transition"></div>
      <template v-for="category in titlesByCategory">
        <titles-row :category="category"></titles-row>
      </template>

      <template v-for="category, index in additionalTitles">
        <titles-row v-if="index < rowsAdded" :category="category"></titles-row>
      </template>
    </div>
    <footer class="footer">
      <div class="footer-fade"></div>
      <loader></loader>
      <div class="footer-info">
        <div class="info-left">MovieDb</div>
        <div class="info-right"><icon name="copyright"></icon>2015 - 2017 MovieDb , inc.</div>
      </div>
      <div class="return" @click="returnToMenu">Return to menu</div>
    </footer>
  </div>
</template>

<script>
import TitlesRow from '@/components/TitlesRow'
import Trailer from '@/components/Trailer'
import Loader from '@/components/Loader'
import titlesByCategory from '@/data/titlesByCategory.js'
import additionalTitles from '@/data/additionalTitles.js'
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

// const imdb = require('imdb-api')

export default {
  name: 'Main',
  components: {
    'titles-row': TitlesRow,
    'trailer': Trailer,
    'loader': Loader,
    'Icon': Icon
  },
  data () {
    return {
      rowsAdded: 0,
      titlesByCategory: titlesByCategory,
      additionalTitles: additionalTitles,
      activeHeroHeader: 'movies',
      activeHeroSub: 'theaters',
      showTrailer: false
    }
  },
  methods: {
    selectHeroHeader: function (tab) {
      this.activeHeroHeader = tab
    },
    selectHeroSub: function (tab) {
      this.activeHeroSub = tab
    },
    playTrailer: function () {
      this.showTrailer = true
    },
    returnToMenu: function () {
      document.body.scrollTop = 0
      document.documentElement.scrollTop = 0
    },
    addRow: function () {
      let self = this
      if ((window.innerHeight + window.scrollY) >= document.body.offsetHeight) {
        setTimeout(function () {
          self.rowsAdded += 1
        }, 400)
      }
    }
  },
  created: function () {
    window.addEventListener('scroll', this.addRow)
  },
  destroyed () {
    window.removeEventListener('scroll', this.addRow)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
// fonts
@import url('https://fonts.googleapis.com/css?family=Roboto|Assistant|Yantramanav|Modak|Poppins|Archivo+Black|Open+Sans:800');

// variables
$brand-red: #da3535;
$brand-red-dark: #b32020;
$light-gold: #f3c532;
$gold: #e2b010;
$light-grey: #eee;

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

.app-container {
  width: 100%;
}

ul {
  padding: 0;
  li {
    display: inline-block;
    &:hover {
      cursor: pointer;
    }
  }
}

.hero {
  position: relative;
  width: 100%;
  font-family: 'Archivo Black';
  letter-spacing: 1px;
  color: #fff;
  .brand {
    position: absolute;
    z-index: 2;
    top: 0.8em;
    left: 1em;
    color: $brand-red;
    font-family: 'Modak';
    font-size: 1.8em;
    cursor: pointer;
  }
  header {
    position: absolute;
    left: 0;
    right: 0;
    text-align: center;
    z-index: 1;
    ul {
      li {
        position: relative;
        text-transform: uppercase;
        font-family: 'Poppins';
        font-size: 0.8em;
        font-weight: 600;
        margin: 1em 0.6em;
        @include transition(all, 0.2s)
        &:after {
          position: absolute;
          margin-top: 3px;
          content: '';
          display: block;
          width: 0;
          height: 2px;
          background-color: $brand-red;
          background-color: #dab847;
          left: 50%;
          @include transform(translateX(-50%));
          @include transition(all, 0.3s)
        }
        &.active,
        &:hover {
          &:after {
            width: 100%;
          }
        }
      }
    }
  }
  img {
    width: 100%;
    //@include transform(scaleX(-1))
  }
  .hero-details {
    position: absolute;
    z-index: 1;
    text-transform: uppercase;
    top: 30%;
    left: 10%;
    h1 {
      font-size: 3em;
      padding-left: 0.1em;
      margin-bottom: 0;
      text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.2);
    }
    ul {
      margin-top: 0;
      li {
        text-shadow: 2px 2px 3px rgba(0, 0, 0, 0.2);
        font-family: 'Archivo Black';
        font-size: 0.7em;
        font-weight: 800;
        margin: 0.4em;
      }
    }
    .trailer-button {
      position: relative;
      display: inline-block;
      font-family: 'Open Sans';
      letter-spacing: 0;
      color: #fff;
      font-size: 0.8em;
      font-weight: 800;
      box-shadow: 0 0 7px 0px rgba(0, 0, 0, 0.3), 0 0 5px 0px rgba(0, 0, 0, 0.1);
      background-color: $brand-red;
      border-radius: 2em;
      padding: 1em 2.5em 1em 1em;
      cursor: pointer;
      @include transition(all, 0.15s);
      span {
        margin-right: 1em;
      }
      &:hover {
        background-color: $brand-red-dark;
      }
      .fa-icon {
        position: absolute;
        top: 50%;
        @include transform(translateY(-50%))
        height: 1.7em;
        width: 1.7em;
      }
    }
  }
  .menu {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: linear-gradient(rgba(0, 0, 0, 0.85) 0%, rgba(0, 0, 0, 0.5) 30%, rgba(0, 0, 0, 0.2) 78%, rgba(0, 0, 0, 0) 100%);
    width: 100%;
    height: 5em;
    &.bottom {
      bottom: 0;
      height: 20%;
      min-height: 75px;
      background: linear-gradient(rgba(0, 0, 0, 0) 0%, rgba(0, 0, 0, 0.9) 40%, rgba(0, 0, 0, 0.98) 85%, rgba(0, 0, 0, 1) 100%);
    }
    .inner {
      margin-top: auto;
      display: inline-block;
      background-color: #fff;
      border-radius: 5px 5px 0 0;
      font-family: 'Poppins';
      letter-spacing: 0;
      ul {
        margin: 0 3em;
        border-bottom: 1px solid $light-grey;
        li {
          margin: 0;
          padding: 1em;
          color: #666a66;
          border-bottom: 2px solid rgba(100, 100, 100, 0);
          @include transition(border-color 0.5s, color 0.5s)
          &.active,
          &:hover {
            color: #333;
            border-color: rgba(100, 100, 100, 1);
          }
        }
      }
    }
  }
}

.titles {
  position: relative;
  z-index: 1;
  overflow-x: hidden;
  padding: 1em 0 0;
  background-color: $light-grey;
  .titles-transition {
    position: absolute;
    z-index: -1;
    display: block;
    top: 0;
    left: 0;
    right: 0;
    height: 10em;
    background: linear-gradient(white, $light-grey)
  }
}

footer {
  position: relative;
  padding-top: 4em;
  border: 1px solid $light-grey;
  font-family: 'Poppins';
  .footer-fade {
    position: absolute;
    height: 4em;
    top: 0;
    width: 100%;
    background: linear-gradient($light-grey, white)
  }
  .footer-info {
    padding: 1em;
    display: flex;
    justify-content: space-between;
    color: #bbb;
    .info-left {
      font-family: 'Modak';
      font-size: 1.5em;
      padding-bottom: 0.2em;
    }
    .info-right {
      position: relative;
      align-self: center;
      font-weight: 700;
      padding-left: 20px;
      .fa-icon {
        position: absolute;
        left: 0;
        top: 50%;
        @include transform(translateY(-50%))
      }
    }
  }
  .return {
    padding: 18px 0;
    text-align: center;
    text-transform: uppercase;
    font-size: 0.8em;
    font-family: 'Poppins';
    font-weight: 700;
    color: $light-gold;
    border-top: 1px solid #eee;
    cursor: pointer;
    &:hover {
      color: $gold;
    }
  }
}
</style>
















