<template>
  <article class="runContainer">
    <span class="imageSpan">
      <img class="image" :src="information.src" alt="" />
      <header class="runHeader">
        <h2 class="heading">{{ information.title }}</h2>
        <p>{{ information.description }}</p>
      </header>
    </span>
  </article>
</template>

<script>
export default {
  name: 'Runs',
  props: {
    information: Object,
  },
  data() {
    return {}
  },
}
</script>

<style scoped>
.runContainer {
  width: 100%;
  height: fit-content;
}

.imageSpan {
  width: 100%;
  height: 80vh;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

.image {
  width: 100%;
}

.runHeader {
  position: absolute;
  right: 50px;
  bottom: 50px;
  width: 250px;
  height: 120px;
  background: #673399bb;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 10px;
  color: white;
}

.heading {
  font-size: 2rem;
  text-transform: uppercase;
  font-weight: 700;
}
</style>
