<template lang="pug">
li
  div(class="card-panel z-depth-3")
    img(v-bind:src="artist.image[2]['#text']" class="circle responsive-img")
    a(v-bind:href="artist.url" target="_blank") {{artist.name}}
    span Listeners: {{artist.listeners}}
  
</template>

<script>
export default {
  name: 'artist',
  props:['artist']
  }
</script>

<style lang="stylus" scoped>
li
  margin 10px 10px
a
  display block
  font-size 15px
  font-weight bold
  
span
  font-size 15px

</style>
