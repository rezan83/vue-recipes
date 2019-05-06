<template>
  <div class="about">
    <About msg="This is the new About page" />
  </div>
</template>
<script>
// @ is an alias to /src
import About from '@/components/About.vue'

export default {
  name: 'home',
  components: {
    About
  }
}
</script>