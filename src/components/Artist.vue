<template>
  <div class="artist" >
    <h4><a :href="artist.url" target="_blank">{{ artist.name }}</a></h4>
    <img :src="artist.image[2]['#text']" alt="">
  </div>
</template>

<script>
export default {
  name: 'Artist',
  props: ['artist']
}
</script>

<style scoped>
.artist {
    display: block;
}
</style>
