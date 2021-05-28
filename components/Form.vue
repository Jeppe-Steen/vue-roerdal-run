<template>
  <form class="pageForm" action="">
    <span class="fieldWrapper">
      <label class="fieldLabel">Vælg løb</label>
      <select
        @change="setDistance"
        name="'Vælg løb'"
        class="inputField requiredRegistration distance"
      >
        <option selected disabled value=""></option>
        <option value="1">One Mile</option>
        <option value="2">Stafetten</option>
        <option value="3">Den lange</option>
      </select>
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Fornavn</label>
      <input
        @keyup="setFirstname"
        name="'Fornavn'"
        class="inputField requiredRegistration firstname"
        type="text"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Efternavn</label>
      <input
        @keyup="setLastname"
        name="'Efternavn'"
        class="inputField requiredRegistration lastname"
        type="text"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Adresse</label>
      <input
        @keyup="setAddress"
        name="'Adresse'"
        class="inputField requiredRegistration address"
        type="text"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Postnummer</label>
      <input
        @keyup="setZipcode"
        name="'Postnummer'"
        class="inputField requiredRegistration zipcode"
        type="number"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">By</label>
      <input
        @keyup="setCity"
        name="'By'"
        class="inputField requiredRegistration city"
        type="text"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Email</label>
      <input
        @keyup="setEmail"
        name="'Email'"
        class="inputField requiredRegistration email"
        type="email"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Telefon</label>
      <input
        @keyup="setPhone"
        name="'Telefon'"
        class="inputField requiredRegistration phone"
        type="number"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Fødselsdato</label>
      <input
        @change="setBirth"
        name="'Fødselsdato'"
        class="inputField requiredRegistration birth"
        type="date"
      />
    </span>
    <span class="fieldWrapper">
      <label class="fieldLabel">Køn</label>
      <span class="radioWrapper">
        <span>
          <input @click="setGender" type="radio" class="male" value="m" />
          <label class="radioLabel">Mand</label>
        </span>
        <span>
          <input @click="setGender" type="radio" class="female" value="f" />
          <label class="radioLabel">Kvinde</label>
        </span>
      </span>
    </span>
    <span class="textWrapper">
      <label class="textLabel">Evt. kommentar</label>
      <textarea @keyup="setComment" class="textField"></textarea>
    </span>
    <span>
      <button type="button" class="btn send" @click="checkInputs">
        Tilemd
      </button>
      <button type="button" class="btn delete" @click="handleDelete">
        Annuler
      </button>
    </span>
  </form>
</template>

<script>
export default {
  name: 'Form',
  data() {
    return {
      distance: 0,
      firstname: '',
      lastname: '',
      address: '',
      zipcode: 0,
      city: '',
      email: '',
      phone: 0,
      birth: 0,
      gender: null,
      comment: '',
    }
  },
  methods: {
    checkInputs() {
      let success = true
      const arrayOfRequired = [
        ...document.querySelectorAll('.requiredRegistration'),
      ]
      for (const element of arrayOfRequired) {
        if (!element.value) {
          success = false
          alert(element.name + ' mangler at blive udfyldt')
          return false
        }
      }

      const maleRadio = document.querySelector('.male')
      const femaleRadio = document.querySelector('.female')

      if (!maleRadio.checked && !femaleRadio.checked) {
        success = false
        alert('Du skal vælge et køn')
        return false
      }

      if (success) {
        this.handleSend()
      }
    },
    handleSend() {
      const formData = new URLSearchParams()
      formData.append('run_id', this.distance)
      formData.append('firstname', this.firstname)
      formData.append('lastname', this.lastname)
      formData.append('address', this.address)
      formData.append('zipcode', this.zipcode)
      formData.append('city', this.city)
      formData.append('email', this.email)
      formData.append('phone', this.phone)
      formData.append('birthdate', this.birth)
      formData.append('gender', this.gender)
      formData.append('comment', this.comment)

      const doFetch = async () => {
        const url = 'https://api.mediehuset.net/rordal/registrations'
        const options = {
          method: 'POST',
          body: formData,
        }
        const response = await fetch(url, options)
        const data = await response.json()
        console.log(data)
        return data
      }
      doFetch()
    },
    handleDelete() {
      console.log('delete')
    },
    setFirstname(e) {
      this.firstname = e.currentTarget.value
    },
    setLastname(e) {
      this.lastname = e.currentTarget.value
    },
    setAddress(e) {
      this.address = e.currentTarget.value
    },
    setZipcode(e) {
      this.zipcode = e.currentTarget.value
    },
    setCity(e) {
      this.city = e.currentTarget.value
    },
    setEmail(e) {
      this.email = e.currentTarget.value
    },
    setPhone(e) {
      this.phone = e.currentTarget.value
    },
    setBirth(e) {
      this.birth = Date.parse(e.currentTarget.value)
    },
    setGender(e) {
      this.gender = e.currentTarget.value
    },
    setComment(e) {
      this.comment = e.currentTarget.value
    },
    setDistance(e) {
      this.distance = e.currentTarget.value
    },
  },
}
</script>

<style scoped>
.pageForm {
  display: flex;
  flex-direction: column;
  width: 50%;
  align-items: flex-end;
}

.fieldWrapper {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 30px;
  margin: 0 0 10px 0;
  background: white;
  border: 1px solid grey;
}
.textWrapper {
  display: flex;
  flex-direction: row;
  width: 100%;
  height: 100px;
  margin: 0 0 10px 0;
  background: white;
  border: 1px solid grey;
}

.fieldWrapper:last-of-type {
  margin: 0;
}

.fieldLabel {
  width: 40%;
  height: 100%;
  background: lightgray;
  display: flex;
  align-items: center;
  justify-content: center;
}

.textLabel {
  width: 40%;
  height: 100%;
  background: lightgray;
  display: flex;
  align-items: flex-start;
  justify-content: center;
  padding: 5px;
}

.inputField {
  width: 60%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  border: none;
  padding: 0 10px;
}

.textField {
  width: 60%;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  border: none;
  padding: 0 10px;
}

.radioWrapper {
  width: 60%;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}

.btn {
  width: 100px;
  padding: 10px;
  color: white;
  border: none;
  text-transform: uppercase;
  cursor: pointer;
}

.send {
  background: green;
}

.delete {
  background: red;
}
</style>
