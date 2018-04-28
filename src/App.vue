<template>
  <div id="app">
    <intro-card
      headline="Alan Richey is a web developer."
      sub-headline="He is also a huge geek that can't dance. Here are some statistics."
    />
  </div>
</template>

<script>
import IntroCard from './components/IntroCard.vue';
import MtgChart from './components/MtgChart.vue';

export default {
  name: 'app',
  components: {
    IntroCard,
    MtgChart,
  },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Alice|Playfair+Display');

#app {
  font-family: 'Alice', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 12px;
}

// Small devices (landscape phones, 576px and up)
// @media (min-width: 576px) { ... }

// Medium devices (tablets, 768px and up)
// @media (min-width: 768px) { ... }

// Large devices (desktops, 992px and up)
// @media (min-width: 992px) { ... }

// Extra large devices (large desktops, 1200px and up)
// @media (min-width: 1200px) { ... }
</style>
