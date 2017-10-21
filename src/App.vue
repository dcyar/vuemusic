<template lang="pug">

  #app
    img(class='logo' src='./dist/logo.jpg')
    h1 VueMusic

    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.name }}

    spinner(v-show="loading")

    ul
      artist(v-for="art in artists" :artist="art" :key="art.mbid") {{ art.name }}

</template>

<script>

  import Artist from './components/Artist.vue'
  import Spinner from './components/Spinner.vue'
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
          { name: 'Argentina', value: 'argentina' },
          { name: 'España', value: 'spain' },
        ],
        selectedCountry: 'peru',
        loading: true,
      };
    },
    components: {
      Artist,
      Spinner
    },
    created() {
      this.refreshArtists()
    },
    methods: {
      refreshArtists() {
        this.loading = true
        this.artists = []
        getArtists(this.selectedCountry)
          .then((artists) => {
            this.loading = false
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
.logo{
  width: 200px;
}
</style>
