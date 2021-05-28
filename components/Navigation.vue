<template>
  <header class="pageNavigation">
    <button class="closeButton" @click="handleClick(false)">X</button>
    <button class="openButton" @click="handleClick(true)">menu</button>
    <nav class="hiddenMenu">
      <ul class="list">
        <li
          v-for="item in navigationList"
          :key="item.index"
          class="menuLinks"
          @click="handleClick(false)"
        >
          <nuxtLink class="links" :to="item.path">
            {{ item.name }}
          </nuxtLink>
        </li>
      </ul>
      <form class="form">
        <input
          class="inputField required"
          type="text"
          placeholder="Intast burgernavn"
          @keyup="setUsername"
        />
        <input
          class="inputField required"
          type="password"
          placeholder="Intast kodeord"
          @keyup="setPassword"
        />
        <button class="submitButton" type="button" @click="handleSubmit">
          Submit
        </button>
      </form>
    </nav>
    <logo />
  </header>
</template>

<script>
import logo from '~/components/Logo'
export default {
  props: {
    logo,
  },
  data() {
    return {
      errorMessage: '',
      visibleMenu: false,
      username: '',
      password: '',
      navigationList: [
        {
          name: 'Forside',
          path: '/',
          index: 0,
        },
        {
          name: 'Om rørdal run',
          path: '/om',
          index: 1,
        },
        {
          name: 'Distancer',
          path: '/distancer',
          index: 2,
        },
        {
          name: 'tilmelding',
          path: '/tilmelding',
          index: 3,
        },
        {
          name: 'Login',
          path: '/',
          index: 4,
        },
      ],
    }
  },
  watch: {
    visibleMenu() {
      const menu = document.querySelector('.hiddenMenu')
      const closeButton = document.querySelector('.closeButton')
      if (this.visibleMenu === false) {
        menu.classList.remove('active')
        closeButton.classList.remove('activeButton')
      } else {
        menu.classList.add('active')
        closeButton.classList.add('activeButton')
      }
    },
    errorMessage() {
      console.log(this.errorMessage)
    },
  },
  methods: {
    handleClick(state) {
      this.visibleMenu = state
    },
    setUsername(e) {
      this.username = e.currentTarget.value
    },
    setPassword(e) {
      this.password = e.currentTarget.value
    },
    checkResults() {
      const message = JSON.parse(sessionStorage.getItem('access_token'))
      if (message.message) {
        alert('username /or password is invalid')
        return false
      }

      if (!message.message) {
        this.$router.push('/tilmeldinger')
        this.handleClick(false)
      }
    },
    handleSubmit() {
      const doFetch = async () => {
        const url = 'https://api.mediehuset.net/token'
        const formData = new URLSearchParams()
        formData.append('username', this.username)
        formData.append('password', this.password)

        const options = {
          method: 'POST',
          body: formData,
        }

        const response = await fetch(url, options)
        const data = await response.json()

        const handleSessionData = () => {
          sessionStorage.setItem(
            'access_token',
            JSON.stringify({
              token: data.access_token,
              message: data.message,
            })
          )
        }

        handleSessionData()
      }
      doFetch()
      setTimeout(() => {
        this.checkResults()
      }, 500)
    },
  },
}
</script>

<style scoped>
.pageNavigation {
  width: 20%;
  right: 0;
  background: #673399;
  height: 100vh;
  color: white;
  display: flex;
  flex-direction: column;
  position: fixed;
  z-index: 8999;
}

.closeButton {
  display: none;
  position: absolute;
  top: 20px;
  left: 30px;
  border: none;
  background: transparent;
  cursor: pointer;
  color: white;
  font-size: 1.5rem;
  z-index: 9001;
  opacity: 0;
}

.activeButton {
  display: flex;
  opacity: 1;
  transition: opacity 0.3s ease-in-out;
}

.openButton {
  position: absolute;
  top: 20px;
  right: 30px;
  border: none;
  background: transparent;
  cursor: pointer;
  color: white;
  font-size: 1.5rem;
}

.hiddenMenu {
  display: none;
  flex-direction: column;
  width: 100%;
  height: 100%;
  background: #673399;
  z-index: 9000;
}

@keyframes slider {
  from {
    transform: translateX(100%);
  }

  to {
    transform: translateX(0%);
  }
}

.active {
  display: flex;
  animation: slider 0.3s;
}

.list {
  margin-top: 100px;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 10px;
  margin: 0 20px;
}

.inputField {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 10px;
  border: none;
}

.submitButton {
  width: 50%;
  padding: 10px;
  border-radius: 10px;
  border: none;
  background: yellow;
}

.menuLinks {
  list-style: none;
  padding: 10px;
  margin: 0 20px;
  border-bottom: 1px solid white;
}

.menuLinks:last-of-type {
  border-bottom: none;
}

.links {
  width: auto;
  height: auto;
  width: 100%;
  color: white;
  text-decoration: none;
  text-transform: uppercase;
}
</style>
