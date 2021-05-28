<template>
  <main>
    <pageHero :information="heroInformation" />
    <pageFooter />
  </main>
</template>

<script>
import pageHero from '~/components/PageHero'
import pageFooter from '~/components/Footer'
import heroPicture from '~/assets/personalRun.jpg'

export default {
  name: 'Om',
  components: {
    pageHero,
    pageFooter,
  },
  data() {
    return {
      title: 'Om Rørdal Run',
      heroInformation: {
        title: '',
        description: '',
        buttonText: '',
        buttonState: false,
        src: heroPicture,
      },
    }
  },
}
</script>

<style></style>
