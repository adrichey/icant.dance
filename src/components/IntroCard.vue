<template>
  <div class="intro-card">
    <header>
      <h1>{{ headline }}</h1>
      <h2>{{ subHeadline }}</h2>
    </header>
  </div>
</template>

<script>
export default {
  name: 'intro-card',
  props: {
    headline: {
      type: String,
      required: true,
    },
    subHeadline: {
      type: String,
      default: '',
    },
  },
};
</script>

<style lang="scss" scoped>
.intro-card {
  height: 100vh;
  width: 100vw;
  position: relative;
  font-size: 12px;

  header {
    position: absolute;
    top: 50%;
    margin: -6em 5% 0 5%;
    width: 90%;

    h1 {
      margin: 0;
      font-family: 'Playfair Display', serif;
      font-size: 3em;
      margin-bottom: .2em;
    }

    h2 {
      margin: 0;
      font-size: 1.2em;
    }
  }
}

@media (min-width: 992px) {
  .intro-card header {
    h1 {
      font-size: 5em;
    }

    h2 {
      font-size: 2em;
    }
  }
}
</style>