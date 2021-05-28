<template>
  <div class="layoutGrid">
    <Navigation />
    <Nuxt />
  </div>
</template>

<script>
import Navigation from '~/components/Navigation'

export default {
  components: {
    Navigation,
  },
  data() {
    return {}
  },
}
</script>

<style>
html {
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

.layoutGrid {
  display: grid;
  grid-template: auto / 80% 20%;
  grid-template-areas: 'main .';
}
</style>
