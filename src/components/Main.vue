<template>
  <div class="app-container">
    <div class="hero">
      <header class="menu">
        <ul>
          <li :class="{ active: activeHeroHeader === 'movies' }" @click="selectHeroHeader('movies')">Movies</li>
          <li :class="{ active: activeHeroHeader === 'photos' }" @click="selectHeroHeader('photos')">Photo Gallery</li>
          <li :class="{ active: activeHeroHeader === 'community' }" @click="selectHeroHeader('community')">Community</li>
          <li :class="{ active: activeHeroHeader === 'news' }" @click="selectHeroHeader('news')">News</li>
        </ul>
      </header>
<!--       <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:100px;">search</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:130px;">horizontal scroll</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:160px">genre</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:190px">search</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:220px">menu</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:250px">footer</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:280px">icons</p>
      <p style="position:absolute;color:#fff;background-color:#666;padding-left:5px;padding-right:5px;left:20px;top:310px">My List</p> -->


      <div class="hero-details">
        <h1>Coco</h1>
        <ul>
          <li>Animation</li>
          <li>Adventure</li>
          <li>Comedy</li>
        </ul>
        <div class="trailer-button"><span>Watch Trailer</span><icon name="play-circle-o"></icon></div>
      </div>
      <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMTg2NTMzNTU2Ml5BMl5BanBnXkFtZTgwNzk4NDMwMTI@._V1_SX1777_CR0,0,1777,788_AL_.jpg" />
      <div class="menu bottom">
        <div class="inner">
          <ul>
            <li :class="{ active: activeHeroSub === 'theaters' }" @click="selectHeroSub('theaters')">In Theaters</li>
            <li :class="{ active: activeHeroSub === 'coming' }" @click="selectHeroSub('coming')">Coming Soon</li>
            <li :class="{ active: activeHeroSub === 'tv' }" @click="selectHeroSub('tv')">TV Series</li>
            <li :class="{ active: activeHeroSub === 'trailers' }" @click="selectHeroSub('trailers')">Trailers</li>
            <li :class="{ active: activeHeroSub === 'more' }" @click="selectHeroSub('more')">More</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="titles">
      <div class="titles-transition"></div>

      <template v-for="titles, categoryName in titleData">
        <titles-row :titles="titles" :categoryName="categoryName"></titles-row>
      </template>
    </div>
    <footer class="footer">
      <div class="footer-fade"></div>
      <ul>
        <li>Careers</li>
        <li>Help Center</li>
        <li>Terms of Use</li>
        <li>Contact Us</li>
        <li>Privacy</li>
        <li>About</li>
      </ul>
    </footer>
  </div>
</template>

<script>
import TitlesRow from '@/components/TitlesRow'
import titlesByCategory from '@/data/titlesByCategory.js'
import 'vue-awesome/icons'
import Icon from 'vue-awesome/components/Icon'

const imdb = require('imdb-api')

export default {
  name: 'Main',
  components: {
    'titles-row': TitlesRow,
    'Icon': Icon
  },
  data () {
    return {
      titleData: {},
      activeHeroHeader: 'movies',
      activeHeroSub: 'theaters'
    }
  },
  methods: {
    selectHeroHeader: function (tab) {
      this.activeHeroHeader = tab
    },
    selectHeroSub: function (tab) {
      this.activeHeroSub = tab
    }
  },
  created: function () {
    const self = this
    titlesByCategory.forEach(function (categoryObj) {
      self.titleData[categoryObj.name] = {}
      categoryObj.titles.forEach(function (title) {
        imdb.get(title,
          { apiKey: '4162605e',
          // { apiKey: 'ac6f6f7b',
            timeout: 30000
          }).then(function (response) {
            self.titleData[categoryObj.name][title] = response
          })
        .catch(console.log)
      })
    })
    console.log(self.titleData)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
// fonts
@import url('https://fonts.googleapis.com/css?family=Roboto|Assistant|Yantramanav');

// variables
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
  font-family: 'Roboto';
  color: #fff;
  header {
    position: absolute;
    left: 0;
    right: 0;
    text-align: center;
    z-index: 1;
    ul {
      li {
        text-transform: uppercase;
        font-family: 'Yantramanav';
        font-size: 0.9em;
        font-weight: 600;
        padding: 1em 0.6em;
        &.active {
          color: red;
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
    }
    ul {
      margin-top: 0;
      li {
        font-family: 'Assistant';
        font-weight: 600;
        margin: 0.4em;
      }
    }
    .trailer-button {
      display: inline-block;
      border: 1px solid #fff;
      border-radius: 2em;
      padding: 0.5em;
      span {
        margin-right: 0.5em;
      }
      .fa-icon {
        //display: inline-block;
        //height: 1.2em;
        //width: 1.2em;
        //@include transform(translateY(12%))
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
      ul {
        margin: 0 3em;
        border-bottom: 1px solid $light-grey;
        li {
          margin: 0;
          padding: 1em;
          color: #666a66;
          border-bottom: 2px solid rgba(100, 100, 100, 0);
          @include transition(border-color 0.5s, color 0.5s)
          &.active {
            color: red;
            border-color: rgba(100, 100, 100, 1);
          }
          &:hover {
            border-color: rgba(100, 100, 100, 1);
            color: rgba(100, 100, 100, 1);
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
  height: 14em;
  border: 1px solid $light-grey;
  .footer-fade {
    position: absolute;
    height: 4em;
    top: 0;
    width: 100%;
    background: linear-gradient($light-grey, white)
  }
  ul {
    color: #444;
  }
}
</style>
















