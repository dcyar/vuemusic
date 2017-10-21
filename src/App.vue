<template lang="pug">

  #app
    img(src='./assets/logo.png')
    h1 VueMusic

    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.name }}

    ul
      artist(v-for="art in artists" :artist="art" :key="art.mbid") {{ art.name }}

</template>

<script>

import Artist from './components/Artist.vue'
import getArtists from './api/api.js'

export default {
  name: "app",
  data() {
    return {
      artists: [],
      countries: [
        { name: 'Perú', value: 'peru' },
        { name: 'Venezuela', value: 'venezuela' },
        { name: 'Colombia', value: 'colombia' },
      ],
      selectedCountry: 'peru',
    };
  },
  components: {
    Artist
  },
  created() {
    this.refreshArtists()
  },
  methods: {
    refreshArtists() {
      getArtists(this.selectedCountry)
        .then((artists) => {
        this.artists = artists
      })
    }
  },
  watch: {
    selectedCountry() {
      this.refreshArtists()
    }
  }
};
</script>

<style lang="stylus">
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

h1, h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
