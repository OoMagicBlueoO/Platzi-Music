<template lang="pug">
  li
    h2: a(:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[2]['#text']")
</template>
<script>
export default {
  name:'artist',
  props: ['artist']
}
</script>

<style lang="stylus" >
li
  display inline-block
  border-radius 5px
  border 1px solid #333
  padding 10px
  margin 10px
  transition 1s
li:hover
  background-color: #333
li h2
  margin 0
li h2 a
  text-decoration none
li img
  border-radius 100px 30px
  transition .5s
li:hover > img
  border-radius 100%
  box-shadow 3px 3px 20px #333
li:hover > h2 a
  font-weight bold
  text-decoration underline
</style>
