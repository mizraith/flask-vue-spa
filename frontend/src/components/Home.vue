
<template>
  <div>
    <p>Home page</p>
    <p>Random number from backend: {{ randomNumber }}</p>
    <button @click="getRandom">New random number</button>
    <h2>Big random number: {{ bigRandomNumber }}</h2>
    <button @click="getBigRandom">Big Random Number</button>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      randomNumber: 0,
      bigRandomNumber: 0
    }
  },
  methods: {
    getRandomInt (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      return Math.floor(Math.random() * (max - min + 1)) + min
    },
    getRandom () {
      // this.randomNumber = this.getRandomInt(1, 100)
      this.randomNumber = this.getRandomFromBackend()
    },
    getBigRandom () {
      this.bigRandomNumber = this.getBigRandomNumberFromBackend()
    },
    getRandomFromBackend () {
      const path = `http://localhost:5000/api/random`
      axios.get(path)
      .then(response => {
        this.randomNumber = response.data.randomNumber
      })
      .catch(error => {
        console.log(error)
      })
    },
    getBigRandomNumberFromBackend () {
      const path = 'http://localhost:5000/api/bigrandom'
      axios.get(path)
        .then(response => {
          this.bigRandomNumber = response.data.bigRandomNumber
        })
        .catch(error => {
          console.log(error)
        })
    }
  },
  created () {
    this.getRandom()
  }
}
</script>
