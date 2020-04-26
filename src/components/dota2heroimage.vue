<template lang="html">
  <img :src="checkForImage"/>
</template>

<script>
import noImage from '@/assets/noimgfnd.jpg'

export default {
  name: 'dota2-hero-image',
  props: ['imageUrl'],
  computed: {
    checkForImage(){
      return this.imageUrl != undefined ? this.imageUrl : noImage;
    }
  }
}
</script>

<style lang="css" scoped>

img {
  height: 110px;
  width: 40px;
  padding-bottom: 15px;
}

</style>
