<template>
  <main>
    <pageHero :information="heroInformation" />
    <pageFooter />
  </main>
</template>

<script>
import pageHero from '~/components/PageHero'
import pageFooter from '~/components/Footer'
import heroPicture from '~/assets/familyRun.jpg'

export default {
  name: 'Distancer',
  components: {
    pageHero,
    pageFooter,
  },
  data() {
    return {
      title: 'Distancer',
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
