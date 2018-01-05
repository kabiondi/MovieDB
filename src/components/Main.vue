<template>
  <div class="app-container" @click="clickAway">
    <trailer v-if="showTrailer" @closeVideo="showTrailer = false"></trailer>
    <div class="hero" :class="{ dimmed: searchedTitle !== null }">
      <div class="brand">MovieDb</div>
      <header class="menu">
        <ul>
          <li :class="{ active: showSearch === false }">Movies</li>
          <!-- <li :class="{ active: activeHeroHeader === 'photos' }" @click="selectHeroHeader('photos')">Photo Gallery</li> -->
          <!-- <li :class="{ active: activeHeroHeader === 'community' }" @click="selectHeroHeader('community')">Community</li> -->
          <!-- <li :class="{ active: activeHeroHeader === 'news' }" @click="selectHeroHeader('news')">News</li> -->
          <li class="search-button" :class="{ active: showSearch === true }" @click.stop="toggleRevealSearch"><icon name="search"></icon>Search</li>
        </ul>
        <div class="search-wrapper" :class="{ active: showSearch === true }" @click.stop>
          <icon name="search"></icon>
          <input ref="searchInput" type="text" v-on:keyup.enter="searchTitle"></input>
        </div>
      </header>
      <transition name="search-results">
        <div v-if="searchedTitle" class="searched-title" @click.stop>
          <div class="close-search" @click="closeSearch"><icon name="close"></icon></div>
          <img v-if="searchedTitle.poster" :src="searchedTitle.poster" />
          <div class="search-info">
            <h2>{{ searchedTitle.title }} <span v-if="searchedTitle.year">({{ searchedTitle.year }})</span></h2>
            <h3 v-if="searchedTitle.rated" class="search-details"><span>{{ searchedTitle.rated }}</span>{{ searchedTitle.runtime }} - {{ searchedTitle.genres }}</h3>
            <p>{{ searchedTitle.plot }}</p>
          </div>
        </div>
      </transition>

      <div class="hero-details">
        <h1>Jumanji</h1>
        <ul>
          <li>Action</li>
          <li>Adventure</li>
          <li>Comedy</li>
        </ul>
        <div class="trailer-button" @click="playTrailer"><span>Watch Trailer</span><icon name="play-circle-o"></icon></div>
      </div>
      <img class="hero-image" src="http://www.wallpapers4k.us/wp-content/uploads/2017/11/jumanji-welcome-to-the-jungle-wallpaper.jpg" />
      <div class="menu bottom">
        <div class="inner">
          <ul>
            <!-- <li :class="{ active: activeHeroSub === 'suggested' }" @click="selectHeroSub('suggested')">Suggested</li> -->
            <li :class="{ active: activeHeroSub === 'suggested' }" @click="selectHeroSub('suggested')">Suggested</li>
            <li :class="{ active: activeHeroSub === 'theaters' }" @click="selectHeroSub('theaters')">In Theaters</li>
            <li :class="{ active: activeHeroSub === 'coming' }" @click="selectHeroSub('coming')">Coming Soon</li>
            <li :class="{ active: activeHeroSub === 'mylist' }" @click="selectHeroSub('mylist')">My List</li>
            <!-- <li :class="{ active: activeHeroSub === 'tv' }" @click="selectHeroSub('tv')">TV Series</li> -->
            <!-- <li :class="{ active: activeHeroSub === 'trailers' }" @click="selectHeroSub('trailers')">Trailers</li> -->
            <li :class="{ active: activeHeroSub === 'more' }" @click="selectHeroSub('more')">More</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="titles">
      <div class="titles-transition"></div>
      <template v-if="_menuCategory">
        <titles-row :category="_menuCategory"></titles-row>
      </template>

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
import menuTitles from '@/data/menuTitles.js'
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

const imdb = require('imdb-api')

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
      menuTitles: menuTitles,
      activeHeroHeader: 'movies',
      activeHeroSub: 'suggested',
      showTrailer: false,
      showSearch: false,
      searchedTitle: null
    }
  },
  methods: {
    toggleRevealSearch: function () {
      const searchInput = this.$refs.searchInput
      if (this.showSearch === true) {
        this.closeSearch()
      } else {
        searchInput.focus()
        this.showSearch = true
      }
    },
    closeSearch: function () {
      const searchInput = this.$refs.searchInput
      searchInput.value = ''
      searchInput.blur()
      this.searchedTitle = null
      this.showSearch = false
    },
    searchTitle: function () {
      const self = this
      let title = self.$refs.searchInput.value
      imdb.get(title,
        // { apiKey: '4162605e',
        { apiKey: 'ac6f6f7b',
          timeout: 5000
        }).then(function (response) {
          self.searchedTitle = response
          console.log(response)
        })
      .catch(function () {
        self.searchedTitle = {
          title: 'No results found for "' + title + '"'
        }
      })
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
    },
    clickAway: function () {
      this.closeSearch()
    }
  },
  computed: {
    _menuCategory () {
      if (this.activeHeroSub === 'theaters') { return this.menuTitles[0] } else
      if (this.activeHeroSub === 'coming') { return this.menuTitles[1] } else
      if (this.activeHeroSub === 'mylist') { return this.menuTitles[2] } else {
        return false
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
$break-large: "1300px";

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
  background-color: #000;
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
    text-shadow: 2px 2px 3px rgba(0, 0, 0, 0.2);
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
      min-height: 44px;
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
        &.search-button {
          position: relative;
          padding-left: 18px;
          .fa-icon {
            position: absolute;
            color: $light-gold;
            width: 14px;
            height: 14px;
            top: 50%;
            left: 0;
            @include transform(translateY(-50%) rotate(90deg));
          }
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
  .hero-image {
    width: 100%;
    opacity: 1;
    @include transition(all 0.2s);
  }
  .hero-details {
    position: absolute;
    z-index: 1;
    text-transform: uppercase;
    top: 30%;
    left: 10%;
    @include transition(all 0.4s);
    transition-delay: 0.4s;
    h1 {
      font-size: 3em;
      padding-left: 0.1em;
      margin-bottom: 0;
      text-shadow: 3px 3px 5px rgba(0, 0, 0, 0.5);
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
  .searched-title {
    position: absolute;
    z-index: 2;
    overflow: hidden;
    top: 150px;
    left: 50%;
    @include transform(translateX(-50%));
    width: 82vw;
    max-width: 830px;
    border-width: 4px;
    border-radius: 4px;
    border-style: solid;
    border-color: rgba(255, 255, 255, 0.2);
    background-color: rgba(0, 0, 0, 0.65);
    padding: 12px;
    height: 24vw;
    max-height: 310px;
    @include transition(all 0.2s ease);
    .close-search {
      position: absolute;
      z-index: 1;
      top: 4px;
      right: 8px;
      padding: 5px;
      cursor: pointer;
      color: #fff;
      opacity: 0.5;
      .fa-icon {
        width: 16px;
        height: 20px;
      }
      &:hover {
        opacity: 0.8;
      }
    }
    img {
      height: 24vw;
      width: 16.1vw;
      max-height: 310px;
      max-width: 208px;
      box-shadow: 0 0 1px 2px rgba(255, 255, 255, 0.1), 0 0 3px 3px rgba(255, 255, 255, 0.1);
    }
    .search-info {
      color: #ddd;
      font-family: 'Roboto';
      display: inline-block;
      vertical-align: top;
      //width: 63vw;
      width: calc(100% - 19vw);
      //max-width: 600px;
      margin-left: 14px;
      opacity: 1;
      padding-left: 0;
      @include transform(translateX(0));
      @include transition(opacity 0.4s, transform 0.4s);
      @media screen and (min-width: $break-large) {
        width: 582px;
      }
      transition-delay: 0.2s;
      h2 {
        font-family: 'Open Sans';
        font-weight: 700;
        margin-top: 0;
        margin-bottom: 10px;
      }
      .search-details {
        font-family: 'Assistant';
        margin-top: 10px;
        span {
          border: 1px solid #ddd;
          margin-right: 10px;
          padding: 2px 8px;
        }
      }
      p {
        height: calc(20vw - 58px);
        max-height: 218px;
        color: #bbb;
        font-family: 'Assistant';
        overflow: auto;
        padding-right: 10px;
      }
      ::-webkit-scrollbar {
        width: 4px;
        background-color: rgba(255, 255, 245, 0.1);
      }
      ::-webkit-scrollbar-thumb {
        background-color: $brand-red-dark;
      }
    }

    // SEARCH RESULTS TRANSITION CLASSES
    &.search-results-enter,
    &.search-results-leave-to {
      opacity: 0;
      .search-info {
        opacity: 0;
      }
    }
    &.search-results-enter {
      height: 2vw;
      padding-left: 100px;
      width: 1%;
      .search-info {
        @include transform(translateX(10%))
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
          @include transition(border-color 0.5s, color 0.5s);
          &.active,
          &:hover {
            color: #333;
            border-color: rgba(100, 100, 100, 1);
          }
        }
      }
    }
    .search-wrapper {
      position: relative;
      display: table;
      color: $gold;
      .fa-icon {
        position: absolute;
        z-index: 1;
        opacity: 0;
        width: 20px;
        height: 20px;
        left: 10px;
        top: 50%;
        @include transform(translateY(-50%));
      }
      input {
        width: 0;
        opacity: 0;
        padding: 12px 8px 12px 50px;
        border-radius: 5px;
        border: none;
        background-color: #000;
        font-size: 16px;
        color: $light-gold;
        font-weight: 700;
        // text-align: center;
        @include transition(all, 0.2s);
        &:focus {
          outline: none;
        }
      }
      &.active {
        .fa-icon {
          opacity: 0.9;
        }
        input {
          width: 250px;
          opacity: 0.85;
        }
      }
    }
  }
  &.dimmed {
    .hero-image {
      opacity: 0.5;
    }
    .hero-details {
      opacity: 0;
      @include transition(all 0.2s)
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
















