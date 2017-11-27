<template>
  <div class="app-container">
    <div class="hero">
      <header class="menu">
        <ul>
          <li>Movies</li>
          <li>Photo Gallery</li>
          <li>Community</li>
          <li>News</li>
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
        <div class="trailer-button">Watch Trailer</div>
      </div>
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMjE4NDgwNzYyM15BMl5BanBnXkFtZTgwNjAzOTc4MjI@._V1_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMjI4MjE1MDE0Ml5BMl5BanBnXkFtZTgwNjcyMTkxMTI@._V1_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMWM4Y2UxMDctMTMzOC00NGI1LWI1NGUtYjQyMTM5YjQzN2E0XkEyXkFqcGdeQXVyNTY4NDc5MDE@._V1_SX1777_CR0,0,1777,999_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BNGZiYWE2Y2UtNTRiOC00YzA0LTg4MTEtZTllZWEzYWI5ZTk0XkEyXkFqcGdeQXVyNzg2ODI2OTU@._V1_SX1777_CR0,0,1777,735_AL_.jpg" /> -->
      <!-- <img src="https://i0.wp.com/media2.slashfilm.com/slashfilm/wp/wp-content/images/ZZ4F1C300D.jpg" /> -->
      <!-- <img src="https://o.aolcdn.com/images/dims?thumbnail=1335%2C600&quality=80&image_uri=https%3A%2F%2Fs.aolcdn.com%2Fhss%2Fstorage%2Fmidas%2F110555ae23b5595872f68b7cc394ca6%2F205752499%2FBlade%2BRunner%2B2049-1.jpg&client=cbc79c14efcebee57402&signature=163698e7b5c13bd9b7412c513bbc86f19da9fe9b" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMjQ4NzA3MzgzNV5BMl5BanBnXkFtZTgwNTEzMjMyNDM@._V1_SX1777_CR0,0,1777,911_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMTgyMTA2ODMxNl5BMl5BanBnXkFtZTgwMzEzMjMyNDM@._V1_SX1777_CR0,0,1777,743_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BNzFiODZiNzYtOGVkOC00MWM0LThlNDgtZDM4ODA5ZWJiZmEyXkEyXkFqcGdeQXVyNTU5MzI1OTM@._V1_.jpg" /> -->
      <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMTg2NTMzNTU2Ml5BMl5BanBnXkFtZTgwNzk4NDMwMTI@._V1_SX1777_CR0,0,1777,788_AL_.jpg" />
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMTY1OTk3MjczNV5BMl5BanBnXkFtZTgwOTA1NzU1MzI@._V1_SX1500_CR0,0,1500,999_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BNDkxNzY5MjIxNF5BMl5BanBnXkFtZTgwNDg5NjUyMjI@._V1_SX1777_CR0,0,1777,744_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BZTM4OTNlYTktMTFhZi00MTNjLWE4ODYtMTZlMWI3ZTUyNDhkXkEyXkFqcGdeQXVyNzg2ODI2OTU@._V1_SX1777_CR0,0,1777,735_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BNGJiOTlmMTktNjJhYi00NmNmLWE4Y2UtYjM3ZWYwNjVjMjU5XkEyXkFqcGdeQXVyNzg2ODI2OTU@._V1_SX1777_CR0,0,1777,739_AL_.jpg" /> -->
      <!-- <img src="https://images-na.ssl-images-amazon.com/images/M/MV5BMTgxNjQ3ODcxMl5BMl5BanBnXkFtZTgwNTE5ODE1MjI@._V1_SX1777_CR0,0,1777,744_AL_.jpg" /> -->
      <div class="menu bottom">
        <div class="inner">
          <ul>
            <li>In Theaters</li>
            <li>Coming Soon</li>
            <li>TV Series</li>
            <li>Trailers</li>
            <li>More</li>
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
    <footer class="footer">Footer</footer>
  </div>
</template>

<script>
import TitlesRow from '@/components/TitlesRow'
import titlesByCategory from '@/data/titlesByCategory.js'

const imdb = require('imdb-api')

export default {
  name: 'Main',
  components: {
    'titles-row': TitlesRow
  },
  data () {
    return {
      titleData: {}
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
@import url('https://fonts.googleapis.com/css?family=Roboto|Sumana|Assistant');

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

//:root {
  //font-family: 'Sumana';
  //font-size: 20px;
//}

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
  color: #fff;
  header {
    position: absolute;
    left: 0;
    right: 0;
    text-align: center;
    z-index: 1;
    ul {
      li {
        padding: 1em;
      }
    }
  }
  img {
    width: 100%;
    //@include transform(scaleX(-1))
  }
  .hero-details {
    font-family: 'Roboto';
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
    }
  }
  .menu {
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: linear-gradient(rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0.5) 30%, rgba(0, 0, 0, 0.2) 70%, rgba(0, 0, 0, 0) 100%);
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
      //border: 2px solid rgba(100, 100, 100, 0.5);
      //border-bottom: none;
      border-radius: 5px 5px 0 0;
      //width: 500px;
      ul {
        //white-space: nowrap;
        margin: 0 3em;
        border-bottom: 1px solid $light-grey;
        //min-width: 30em;
        //align-items: center;
        //display: flex;
        //justify-content: center;
        li {
          //white-space: nowrap;
          margin: 0;
          padding: 1em;
          color: #666a66;
          border-bottom: 2px solid rgba(100, 100, 100, 0);
          @include transition(border-color 0.5s, color 0.5s)
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
  padding: 1em 0 5em;
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
  height: 14em;
  border: 1px solid $light-grey;
}
</style>
















