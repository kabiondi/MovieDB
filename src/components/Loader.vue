<template>
  <div class="loader">
    <div class="blocks">
      <div class="block"></div>
      <div class="block"></div>
      <div class="block"></div>
      <div class="block"></div>
      <div class="block"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Loader'
}
</script>

<style lang="scss" scoped>
@mixin animation($str) {
  -webkit-animation: #{$str};
  animation: #{$str};      
}

@mixin animation-delay($time) {
  -webkit-animation-delay: #{$time};
  animation-delay: #{$time};
}

.loader {
  text-align: center;
  .blocks {
    display: inline-block;
    .block {
      display: inline-block;
      width: 1em;
      height: 1.4em;
      margin: 0.1em;
      margin-bottom: 0;
      background-color: #ccccdd;
      opacity: 0;
      @include animation(show 1.2s linear infinite)
      &:nth-child(1) {
        @include animation-delay(-0.5s);
      }
      &:nth-child(2) {
        @include animation-delay(-0.4s);
      }
      &:nth-child(3) {
        @include animation-delay(-0.3s);
      }
      &:nth-child(4) {
        @include animation-delay(-0.2s);
      }
      &:nth-child(5) {
        @include animation-delay(-0.1s);
      }
    }
  }
 }

@-webkit-keyframes show {
  0% { opacity: 0; }
  30% { opacity: 1; }
  90% { opacity: 1; }
  100% { opacity: 0; }
}

@keyframes show {
  0% { opacity: 0; }
  30% { opacity: 1; }
  90% { opacity: 1; }
  100% { opacity: 0; }
}
</style>









