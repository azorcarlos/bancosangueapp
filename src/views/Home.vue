<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <Upload msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Upload from '@/components/Upload.vue'

export default {
  name: 'Home',
  components: {
    Upload
  }
}
</script>
