<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Alice|Playfair+Display');

$purple: rgb(58, 23, 76); //#3a174c

#app {
  font-family: 'Alice', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-size: 12px;
  color: $purple;
  background-color: lighten($purple, 80%);
}
</style>

<template>
  <div id="app">
    <intro-card
      headline="Alan Richey is a web developer."
      sub-headline="He also plays a lot of Magic: the Gathering and never went to a school dance."
    />
    <hamburger-navigation />
  </div>
</template>

<script>
import HamburgerNavigation from './components/HamburgerNavigation.vue';
import IntroCard from './components/IntroCard.vue';

export default {
  name: 'app',
  components: {
    HamburgerNavigation,
    IntroCard,
  },
}
</script>
