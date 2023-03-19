<template>
  <PixJs id="app"/>
</template>

<script>
import { defineComponent } from 'vue'
import PixJs from './components/Pix.vue'

export default defineComponent({
  name: 'App',
  components: {
    PixJs
  }
})
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
