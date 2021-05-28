<template>
  <main>
    <pageHero :information="heroInformation" />
    <section class="pageBanner">
      <h1 class="bannerHeader">Rørdal Run 2021</h1>
      <p class="bannerText">
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Harum velit
        officia tenetur facilis in nihil perferendis voluptates vitae quia
        incidunt cum magni tempora, aliquid nesciunt dolorum, mollitia amet.
        Aut, quos! Lorem ipsum, dolor sit amet consectetur adipisicing elit.
        Harum velit officia tenetur facilis in nihil perferendis voluptates
        vitae quia incidunt cum magni tempora, aliquid nesciunt dolorum,
        mollitia amet. Aut, quos!
      </p>
    </section>
    <section class="runSection">
      <runs v-for="run in arrayOfRuns" :key="run.id" :information="run" />
    </section>
    <pageFooter />
  </main>
</template>

<script>
import pageHero from '~/components/PageHero'
import runs from '~/components/Runs'
import pageFooter from '~/components/Footer'
import heroPicture from '~/assets/frontpageHero.jpg'

import oneMilePicture from '~/assets/familyRun.jpg'
import stafettenPicture from '~/assets/corporationRun.jpg'
import denLangePicture from '~/assets/personalRun.jpg'

export default {
  name: 'Forside',
  components: {
    pageHero,
    runs,
    pageFooter,
  },
  data() {
    return {
      title: 'Forside',
      heroInformation: {
        title: 'Rørdal Run 2021',
        description: 'TIlmeld dig, familien eller kollegaernetil årets løb',
        buttonText: 'Tilmelding',
        buttonState: true,
        src: heroPicture,
      },
      arrayOfRuns: [
        {
          id: 1,
          title: 'One mile',
          description: 'et løb for hele familien',
          src: oneMilePicture,
          fullDescription: '',
          details: {
            distance: 1.6,
            depoter: 0,
            height: 40,
          },
        },
        {
          id: 2,
          title: 'Stafetten',
          description: 'et løb for virksomheder',
          src: stafettenPicture,
          fullDescription: '',
          details: {
            distance: 5,
            depoter: 0,
            height: 123,
          },
        },
        {
          id: 3,
          title: 'Den lange',
          description: 'plads til personlige rekorder',
          src: denLangePicture,
          fullDescription: '',
          details: {
            distance: 10,
            depoter: 1,
            height: 220,
          },
        },
      ],
    }
  },
}
</script>

<style scoped>
.pageBanner {
  width: 100%;
  height: fit-content;
  padding: 80px 150px;
}

.bannerHeader {
  font-size: 4rem;
  margin-bottom: 10px;
  text-transform: uppercase;
}

.bannerText {
  font-size: 1.2rem;
}

.runSection {
  width: 100%;
  height: fit-content;
}
</style>
