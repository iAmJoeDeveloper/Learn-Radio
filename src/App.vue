<template lang="pug">
#app
  h1 'Music FM'
  
  div.container
    div(class="row")
      .input-field.col.s4.offset-s4
        select(name="ciudad" id="paises" v-model="selectedCountry")
          option(v-for="country in countries" v-bind:value="country.value") {{country.name}}

  loader(v-show="loading")
  ul
    artist(v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid")
  
</template>

<script>

import Loader from './components/Loader.vue'
import Artist from './components/Artist.vue'
import getArtists from './api'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries:[{
        name: 'España', value: 'spain'
      },{
        name: 'Argentina', value: 'argentina'
      },{
        name: 'Venezuela', value: 'venezuela'
      }],
      selectedCountry:'spain',
      loading: true
    }
  },
  methods:{
    refreshArtists: function(){
      this.loading=true
      this.artists=[]
      const self = this
      getArtists(this.selectedCountry)
        .then(function (artists){
          self.loading = false
          self.artists = artists
      })
    },
    rendering: function(){
      var options = 'l'
      var elem = document.querySelector('#paises')
      var instance = M.FormSelect.init(elem, options)
    }
  },
  components:{
    Artist,
    Loader
  },
  mounted(){
    this.refreshArtists()
    this.rendering()
  },
  watch:{
    selectedCountry(){
      this.refreshArtists()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px

h1, h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color #42b983


</style>
