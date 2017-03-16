<template>
  <div id="app">
    
    <div class="row align-center text-center">
      <div class="column small-12">
        <h1>Cat of the day!</h1>
      </div>
    </div>

    <div class="row align-center text-center">
      <div class="column small-8 medium-6 large-4">
        <a @click="getCat" class="button expanded">Get the cat of the day</a>
      </div>
    </div>

    <div v-if="!error"
      class="row align-center text-center">
      <div class="column small-10 medium-8 large-6">
        <img :src="cat.source">
      </div>
    </div>

    <div v-else
      class="row align-center text-center">
      <div class="column small-12">
        <h3>{{ 'Error: ' + errorMsg }}</h3>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'app',
  data () {
    return {
      cat: {
        source: ''
      },
      error: false,
      errorMsg: ''
    }
  },
  methods: {
    getCat () {
      var _this = this
      axios.get('https://nijikokun-random-cats.p.mashape.com/random', {
        headers: {
          'X-Mashape-Key': 'ANFifkAkMgmshi7jrGvdfzOlZiUHp1kRCOPjsnBUnvhsM6VDXy',
          'Accept': 'application/json'
        }
      }).then(function(response) {
        _this.error = false
        _this.cat = response.data
      }, function(error) {
        _this.error = true
        _this.errorMsg = error.message
      })
      
    }
  }
}
</script>

<style lang="scss">

</style>
