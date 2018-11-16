# appshake package cloudinary vue

## Installation

```
appshake package:add Queue-Inc/appshake-package-cloudinary-vue
```

## Setup environment variables

### Cloudinary variables

```
appshake set VUE_APP_CLOUDINARY_NAME your_cloudinary_name
```

```
appshake set VUE_APP_CLOUDINARY_UPLOAD_PRESET your_cloudinary_upload_preset
```

```
appshake set VUE_APP_CLOUDINARY_FOLDER your_cloudinary_folder_name
```

## Import to your view file

### Web
```App.vue
<template lang="pug">
  #app
    cloudinary-button(
      @start="startUpload"
      @finish="finishUpload"
    ) upload
</template>
<script>
import CloudinaryButton from '@P/components/atoms/CloudinaryButton.vue'
export default {
  components: {
    CloudinaryButton
  },
  methods: {
    startUpload () {
      console.log('start uploading')
    },
    finishUpload () {
      console.log('finish uploading')
    }
  }
}
</script>
```

### Admin
```App.vue
<template lang="pug">
  #app
    cloudinary-album
</template>
<script>
import CloudinaryAlbum from '@P/components/organisms/CloudinaryAlbum.vue'
export default {
  components: {
    CloudinaryAlbum
  }
}
</script>
<style lang="stylus">
</style>
```

## Classes

### web/src/packages/atoms/CloudinaryButton.vue

| Class name | target |
| :--- | ---: |
| .cloudinary-button | Upload button |

### admin/src/packages/organisms/CloudinaryAlbum.vue

| Class name | target |
| :--- | ---: |
| .cloudinary-album-wrapper | Album image |

## Events

### web/src/packages/atoms/CloudinaryButton.vue

| Event | target |
| :--- | ---: |
| start | Fire when the uploading started |
| finish | Fire when the uploading finished |