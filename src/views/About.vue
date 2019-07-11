<template>
  <div class="about">
    <About msg="Make and edit your own recipes" />
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