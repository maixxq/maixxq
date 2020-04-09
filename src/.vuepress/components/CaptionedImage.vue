<template>
  <figure>
    <img :src="imagesrc" alt=""/>
    <figcaption>{{ caption }} - {{ src }}</figcaption>
  </figure>
</template>
<script>
export default {
  props: ['src', 'caption'],
  computed: {
    imagesrc () {
      return './' + this.src
    }
  }
}
</script>