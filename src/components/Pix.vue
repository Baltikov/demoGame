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

    //  add assets text-counter
    this.counterText = new PIXI.Text('0', { fontSize: 24, fill: 0x121212 })
    this.counterText.x = 152
    this.counterText.y = 68
    this.counterText.style.fontSize = 22

    this.recordText = new PIXI.Text('0', { fontSize: 24, fill: 0x121212 })
    this.recordText.x = 215
    this.recordText.y = 68
    this.recordText.style.fontSize = 22

    this.recordText.text = localStorage.getItem('record') || '0'

    //  add assets backgound, cloud
    const sprite = PIXI.Sprite.from('/back.png')

    const headerCloud = PIXI.Sprite.from('/header-cloud.png')
    headerCloud.y = 10

    const headerCounter = PIXI.Sprite.from('/header-counter.png')
    headerCounter.x = 20
    headerCounter.y = 50

    //  add assets sprite ballons
    const blueBaloon = PIXI.Sprite.from('/blue-baloon.png')
    const blueBaloon2 = PIXI.Sprite.from('/blue-baloon.png')
    const blueBaloonSm = PIXI.Sprite.from('/blue-baloon-sm.png')

    const pinkBalloons = []
    for (let i = 0; i < 3; i++) {
      pinkBalloons.push(PIXI.Sprite.from('/ping-baloon.png'))
      this.app.stage.addChild(pinkBalloons[i])
    }

    const yellowBalloons = []
    for (let i = 0; i < 4; i++) {
      yellowBalloons.push(this.createBaloon())
    }

    this.app.stage.addChild(sprite, blueBaloon, blueBaloon2, blueBaloonSm, pinkBalloons[0], pinkBalloons[1], pinkBalloons[2], yellowBalloons[0], yellowBalloons[1], yellowBalloons[2], yellowBalloons[3])
    this.app.stage.addChild(headerCloud, headerCounter, this.counterText, this.recordText)

    // ticker
    // TO DO обернуть в функцию, на текущий момент не расширяемо

    let elapsed = 0.0
    this.app.ticker.add((delta) => {
      elapsed += delta

      yellowBalloons[0].x = 10
      yellowBalloons[0].y = 700 - Math.tan(elapsed / 150) * 815

      yellowBalloons[1].x = 234
      yellowBalloons[1].y = 605 - Math.tan(elapsed / 114) * 615

      yellowBalloons[2].x = 111
      yellowBalloons[2].y = 605 - Math.tan(elapsed / 106) * 815

      yellowBalloons[3].x = 177
      yellowBalloons[3].y = 405 - Math.tan(elapsed / 106) * 415

      blueBaloonSm.x = 199
      blueBaloonSm.y = 311 - Math.tan(elapsed / 189) * 615

      blueBaloon.x = 60
      blueBaloon.y = 400 - Math.tan(elapsed / 100) * 815

      blueBaloon2.x = 180
      blueBaloon2.y = 833 - Math.tan(elapsed / 100) * 715

      pinkBalloons[0].x = 260
      pinkBalloons[0].y = 200 - Math.tan(elapsed / 120) * 515

      pinkBalloons[1].x = 45
      pinkBalloons[1].y = 700 - Math.tan(elapsed / 144) * 815

      pinkBalloons[2].x = 115
      pinkBalloons[2].y = 440 - Math.tan(elapsed / 144) * 515
    })
  },
  methods: {
    baloonHandler (burstBaloon) {
      // save record
      const count = Number(this.counterText.text) + 10
      this.counterText.text = count.toString()
      if (Number(this.recordText.text) < count) {
        localStorage.setItem('record', this.counterText.text)
      }
      // play animesptie
      burstBaloon.play()
      burstBaloon.interactive = false
      setTimeout(() => {
        burstBaloon.visible = false
      }, 700)
      setTimeout(() => {
        burstBaloon.interactive = true
        burstBaloon.stop()
        burstBaloon.gotoAndStop(0)
        burstBaloon.visible = true
      }, 2000)
    },

    createBaloon () {
      const burstBaloon = new AnimatedSprite(this.loadBaloonsSprite())
      burstBaloon.animationSpeed = 0.2
      burstBaloon.loop = false
      burstBaloon.interactive = true
      burstBaloon.on('pointerdown', () => {
        this.baloonHandler(burstBaloon)
      })
      return burstBaloon
    },

    loadBaloonsSprite () {
      const alienImages = [
        '/image_sequence_01.png',
        '/image_sequence_02.png',
        '/image_sequence_03.png',
        '/image_sequence_04.png',
        '/image_sequence_05.png',
        '/image_sequence_06.png',
        '/image_sequence_07.png',
        '/image_sequence_08.png',
        '/image_sequence_09.png',
        '/image_sequence_10.png'
      ]
      const burstBaloon = []

      for (let i = 0; i < 10; i++) {
        const texture = Texture.from(alienImages[i])
        burstBaloon.push(texture)
      }
      return burstBaloon
    }
  }
}

</script>
