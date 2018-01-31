<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Platzi-Music
    p Top de artistas mas populares de acuerdo a el nombre de la ciudad.
    select(v-model="countrySelected")
      option(v-for="country in  countries" :value="country.value") {{ country.name }}
    loader(v-show="loading")
    ul
      artist(v-for='artist in artists' v-bind:artist="artist" v-bind:key="artist.mbid") {{ artist.name}}


</template>
<script>
import Artist from './components/Artist.vue'
import getArtists from './api';
import Loader from './components/Loader.vue'
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries:[
        {name:'Mexico', value:'mexico'},
        {name:'Argentina', value:'argentina'},
        {name:'España', value:'spain'},
      ],
      countrySelected:'mexico',
      loading: true,
    }
  },
  components:{
    Artist,Loader
  },
  methods:{
    reloadCountry(){
      const self = this
      this.loading = true
      this.artists=[]
      getArtists(this.countrySelected)
      .then(function(artists){
        self.artists = artists
        self.loading=false
      })
    }
  },
  mounted: function(){
    this.reloadCountry();
  },
  watch:{
    countrySelected(){
      this.loading = false
      this.reloadCountry()
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
  overflow hidden

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
