<template lang="pug">
div
  input(
    type="file"
    ref="fileInput"
    style="display: none;"
    @change="fileChanged"
  )
  button.cloudinary-button(
    @click="uploadButton"
    :disabled="loading"
  )
    slot
</template>
<script>
import axios from 'axios'
const cloudinaryUrl = `https://api.cloudinary.com/v1_1/${process.env.VUE_APP_CLOUDINARY_NAME}/image/upload`
// VUE_APP_CLOUDINARY_FOLDER
export default {
  data () {
    return {
      loading: false
    }
  },
  methods: {
    uploadButton () {
      this.$refs.fileInput.click()
    },
    fileChanged ($e) {
      this.uploadToCloudinary($e.target.files[0])
    },
    uploadToCloudinary (file) {
      this.loading = true
      this.$emit('start')

      let params = new FormData()
      params.append('file', file)
      params.append('upload_preset', process.env.VUE_APP_CLOUDINARY_UPLOAD_PRESET)

      if (process.env.VUE_APP_CLOUDINARY_FOLDER) {
        params.append('folder', process.env.VUE_APP_CLOUDINARY_FOLDER)
        params.append('tags', [process.env.VUE_APP_CLOUDINARY_FOLDER])
      }

      axios.post(cloudinaryUrl, params)
        .then((response) => {
          this.$emit('finish')
        })
        .catch((error) => {
          this.$emit('finish')
          throw (error)
        })
    }
  }
}
</script>
<style lang="stylus">
</style>
