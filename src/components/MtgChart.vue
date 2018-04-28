<template>
  <div class="mtg-chart">
    <h3>He has <span>9</span> Magic: the Gathering decks.</h3>
    <span class="info">Number of cards in each color across all decks</span>
    <div class="chart">
      <div class="bar bar-0" style="height: 72%;">
        <i class="ms ms-w"></i>
      </div>
      <div class="bar bar-1" style="height: 80%;">
        <i class="ms ms-u"></i>
      </div>
      <div class="bar bar-2" style="height: 60%;">
        <i class="ms ms-b"></i>
      </div>
      <div class="bar bar-3" style="height: 40%;">
        <i class="ms ms-r"></i>
      </div>
      <div class="bar bar-4" style="height: 72%;">
        <i class="ms ms-g"></i>
      </div>
      <div class="bar bar-5" style="height: 16%;">
        <i class="ms ms-c"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'mtg-chart',
};
</script>

<style lang="scss" scoped>
$mtg-bar-width: (100% / 6);

$white: rgb(238, 238, 238);
$black: rgb(38, 38, 38);
$blue: rgb(63, 137, 255);
$red: rgb(255, 61, 61);
$green: rgb(95, 216, 99);
$beige: rgb(201, 186, 169);

.mtg-chart {
  height: 60vh;
  width: 100vw;

  .info {
    float: left;
    position: relative;
    width: 25%;
    height: 100%;
    background: red;

    h1 {
      display: block;
      position: absolute;
      bottom: 0;
      margin: 0;
      height: 100%;
      width: 100%;
      font-family: 'Playfair Display', serif;
      font-size: 3em;

      span {
        width: 100%;
        display: block;
        font-size: 4em;
      }
    }
  }

  .chart {
    position: relative;
    float: right;
    width: 75vw;
    height: 100%;

    .bar {
      position: absolute;
      bottom: 0;
      width: $mtg-bar-width;

      &.bar-0 {
        margin-left: 0;
        background: $white;
        outline: 1px solid darken($white, 10%);
        border-top: 1px solid lighten($white, 10%);
      }

      &.bar-1 {
        margin-left: $mtg-bar-width;
        background: $blue;
        outline: 1px solid darken($blue, 10%);
        border-top: 1px solid lighten($blue, 10%);
      }

      &.bar-2 {
        margin-left: ($mtg-bar-width * 2);
        background: $black;
        outline: 1px solid darken($black, 10%);
        border-top: 1px solid lighten($black, 10%);
      }

      &.bar-3 {
        margin-left: ($mtg-bar-width * 3);
        background: $red;
        outline: 1px solid darken($red, 10%);
        border-top: 1px solid lighten($red, 10%);
      }

      &.bar-4 {
        margin-left: ($mtg-bar-width * 4);
        background: $green;
        outline: 1px solid darken($green, 10%);
        border-top: 1px solid lighten($green, 10%);
      }

      &.bar-5 {
        margin-left: ($mtg-bar-width * 5);
        background: $beige;
        outline: 1px solid darken($beige, 10%);
        border-top: 1px solid lighten($beige, 10%);
      }

      i {
        position: absolute;
        bottom: 0;
        margin-left: -1em;
        margin-bottom: 0.5em;
        line-height: inherit;

        &::before {
          font-size: 2em;
        }
      }
    }
  }
}

// Small devices (landscape phones, 576px and up)
@media (min-width: 576px) {
  .mtg-chart .chart .bar i {
    margin-left: -2em;

    &::before {
      font-size: 4em;
    }
  }
}
</style>