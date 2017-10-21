<template lang="pug">

  li
    img(:src="artist.image[2]['#text']")
    h4: a(:href="artist.url" target="_blank") {{ artist.name }}

</template>

<script>
  export default {
    name: 'artist',
    props: ['artist'],
  };
</script>

<style lang="stylus" scoped>
li
  display inline-block
  border 1px solid
  margin 10px 1px
</style>
