<template>
  <main>
    <pageHero :information="heroInformation" />
    <section class="formContainer">
      <header class="containerHeader">
        <h1 class="heading">
          {{ Heading }}
        </h1>
        <p class="subHeading">
          {{ subHeading }}
        </p>
      </header>
      <div class="wrapper">
        <formField />
      </div>
    </section>
    <pageFooter />
  </main>
</template>

<script>
import pageHero from '~/components/PageHero'
import formField from '~/components/Form'
import pageFooter from '~/components/Footer'
import heroPicture from '~/assets/signUp.jpg'

export default {
  name: 'Tilmelding',
  components: {
    pageHero,
    formField,
    pageFooter,
  },
  data() {
    return {
      heroInformation: {
        title: '',
        description: '',
        buttonText: '',
        buttonState: false,
        src: heroPicture,
      },
      Heading: 'Tilmelding',
      subHeading: 'Vælg distance og deltager og send din tilmelding',
    }
  },
}
</script>

<style scoped>
.formContainer {
  width: 100%;
  height: fit-content;
}

.containerHeader {
  width: 100%;
  height: fit-content;
  padding: 0 50px;
}

.heading {
  text-transform: uppercase;
  font-size: 3rem;
}

.subHeading {
  font-size: 1.2rem;
  margin: 10px 0;
}

.wrapper {
  width: 100%;
  height: fit-content;
  padding: 20px 50px;
}
</style>
