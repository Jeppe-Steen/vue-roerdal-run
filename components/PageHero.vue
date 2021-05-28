<template>
  <section class="pageHero">
    <h2 class="pageHeroTitle">
      {{ information.title }}
    </h2>
    <p class="pageHeroDescription">
      {{ information.description }}
    </p>
    <nuxt-link class="pageHeroButton" :to="'/' + information.buttonText">
      {{ information.buttonText }}
    </nuxt-link>
  </section>
</template>

<script>
export default {
  name: 'PageHero',
  props: {
    information: Object,
  },
  data() {
    return {
      buttonState: this.information.buttonState,
    }
  },
  mounted() {
    const hero = document.querySelector('.pageHero')
    hero.style.backgroundImage = `url(${this.information.src})`
    const button = document.querySelector('.pageHeroButton')
    if (this.buttonState === false) {
      button.style.display = 'none'
    } else {
      button.style.display = 'flex'
    }
  },
}
</script>

<style scoped>
.pageHero {
  background: lightcoral;
  width: 100%;
  height: 80vh;
  clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 80%);
  background-position: 50% 30%;
  background-size: cover;
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column;
  padding: 100px 50px;
}

.pageHeroTitle {
  color: white;
  font-weight: 300;
}

.pageHeroDescription {
  font-size: 3rem;
  color: white;
  width: 45%;
  margin: 20px 0;
}

.pageHeroButton {
  width: 150px;
  padding: 10px;
  border: none;
  height: 50px;
  background: #673399;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-transform: uppercase;
  text-decoration: none;
}
</style>
