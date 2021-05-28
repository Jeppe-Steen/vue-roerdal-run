<template>
  <main class="pageContent">
    <pageHero :information="heroInformation" />
    <section class="listContainer">
      <header class="containerHeader">
        <h1 class="title">
          {{ Heading }}
        </h1>
        <p class="subTitle">
          {{ subHeading }}
        </p>
      </header>
      <ul class="pageTable">
        <li class="rowContainer tableHeader">
          <ul class="tableRow">
            <li></li>
            <li>Id</li>
            <li>Navn</li>
            <li>Post & by</li>
            <li>Distance</li>
          </ul>
        </li>
        <li
          v-for="item in arrayOfRegistrations"
          :key="item.id"
          class="rowContainer"
        >
          <ul class="tableRow">
            <li class="trash" @click="handleDelete(item.id)">trash</li>
            <li>{{ item.id }}</li>
            <li>{{ item.firstname }} {{ item.lastname }}</li>
            <li>{{ item.zipcode }} {{ item.city }}</li>
            <li>{{ item.run_id }}</li>
          </ul>
        </li>
      </ul>
    </section>
    <pageFooter />
  </main>
</template>

<script>
import pageHero from '~/components/PageHero'
import pageFooter from '~/components/Footer'
import heroPicture from '~/assets/participant.jpg'

export default {
  name: 'Tilmeldinger',
  components: {
    pageHero,
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
      Heading: 'Deltagerliste',
      subHeading: 'Her kan du sorterer og administrere løbets deltagere',
      arrayOfRegistrations: [],
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      const fetching = async () => {
        const response = await fetch(
          'https://api.mediehuset.net/rordal/registrations'
        )
        const data = await response.json()
        this.arrayOfRegistrations = [...data.items]
      }
      fetching()
    },
    handleDelete(id) {
      const userId = id

      const deleteFetch = async () => {
        const key = JSON.parse(sessionStorage.getItem('access_token'))
        const url = `https://api.mediehuset.net/rordal/registrations/${userId}`

        const options = {
          method: 'DELETE',
          headers: {
            authorization: `Bearer ${key.token}`,
          },
        }
        const response = await fetch(url, options)
        const data = response.json()
        console.log(data)
      }
      deleteFetch()
      // siden vil ikke opdaterer listen på andre måder
      setTimeout(() => {
        this.$router.go()
      }, 500)
    },
  },
}
</script>

<style scoped>
.pageContent {
  width: 100%;
  height: fit-content;
}

.listContainer {
  width: 100%;
  height: fit-content;
  padding: 0 20px 50px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.containerHeader {
  width: 95%;
  margin-bottom: 20px;
}

ul {
  list-style: none;
}

.pageTable {
  width: 95%;
  height: fit-content;
  background: lightgrey;
  display: flex;
  flex-direction: column;
}

.tableHeader {
  text-transform: uppercase;
  background: grey;
}

.rowContainer {
  padding: 10px;
}

.tableRow {
  width: 100%;
  display: grid;
  grid-template-columns: 1fr 1fr 2fr 3fr 1fr;
}

.title {
  font-size: 3rem;
  text-transform: uppercase;
  margin-bottom: 10px;
}

.subTitle {
  font-size: 1.2rem;
}

.trash {
  cursor: pointer;
}
</style>
