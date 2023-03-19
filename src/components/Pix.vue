<template>
   <div class="connections">
    <canvas id="pixi">
        dsad
    </canvas>
  </div>
</template>

<script>
import * as PIXI from 'pixi.js'
import { AnimatedSprite, Texture } from 'pixi.js'

export default {
  name: 'pixJs',
  data () {
    return {
      counterText: '',
      recordText: ''

    }
  },
  mounted () {
    const canvas = document.getElementById('pixi')
    this.app = new PIXI.Application({
      width: 375,
      height: 812,
      antialias: true,
      transparent: true,
      view: canvas
    })
  }
}

</script>
