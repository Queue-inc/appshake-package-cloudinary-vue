<template lang="pug">
div
  .cloudinary-album-wrapper(v-for="image in imageList")
    img(:src="getImageUrl(image)")
</template>
<script>
import axios from 'axios'
const cloudinaryUrl = `https://res.cloudinary.com/${process.env.VUE_APP_CLOUDINARY_NAME}/image/list/${process.env.VUE_APP_CLOUDINARY_FOLDER}.json`
// VUE_APP_CLOUDINARY_FOLDER
export default {
  data () {
    return {
      loading: false,
      imageList: null
    }
  },
  mounted () {
    this.fetchImages()
  },
  methods: {
    fetchImages () {
      axios.get(cloudinaryUrl)
        .then(response => {
          console.log(response.data)
          this.imageList = response.data.resources
        })
    },
    getImageUrl (imageObj) {
      return `https://res.cloudinary.com/queue-inc/image/upload/v${imageObj.version}/${imageObj.public_id}.${imageObj.format}`
    }
  }
}
// https://res.cloudinary.com/queue-inc/image/upload/1542344234/appshake/b7bpwyue8q9cvxurstag.jpg
// https://res.cloudinary.com/queue-inc/image/upload/v1542344234/appshake/b7bpwyue8q9cvxurstag.jpg
</script>
<style lang="stylus">
.cloudinary-album-wrapper
  display flex
  justify-content center
  align-items center
  float left
  @media screen and (max-width: 480px)
    width 100%
    max-height 480px
  @media screen and (min-width: 480px) and (max-width 600px)
    width 49%
    max-height 300px
  @media screen and (min-width: 600px) and (max-width 960px)
    width 33%
    max-height 240px
  @media screen and (min-width: 960px) and (max-width 1280px)
    width 25%
    max-height 320px
  @media screen and (min-width: 1280px)
    width 20%
    max-height 400px
</style>
