<template>
  <div>
    NOW {{index}}
    <button @click="reset">Reset</button>
    <button @click="previous" v-if="index >= 1">Previous</button>
    <button @click="next">Next</button>
    <img src="">
    <vue-p5
        @setup="setup"
        @draw="draw"
        @keypressed="keyPressed"
        @mousemoved="mouseMoved"
        @mousedragged="mouseDragged"
    >
    </vue-p5>
    {{ lines }}
  </div>
</template>

<script>
import VueP5 from "vue-p5"
// import xxx from '@/assets/data.json'

export default {
  name: "p5-example",
  components: {
    "vue-p5": VueP5
  },
  data: () => ({
    width: 800,
    height: 400,
    lines: [[], []],
    index: 0,
  }),
  methods: {
    setup(sketch) {
      sketch.createCanvas(this.width, this.height)
    },
    draw(sketch) {
      sketch.background(220, 220, 220)

      for (let line of this.lines[this.index]) {
        sketch.stroke(line.color)
        sketch.line(line.pmouseX, line.pmouseY, line.mouseX, line.mouseY)
      }
    },
    keyPressed({ keyCode }) {

    },
    mouseMoved({ mouseX, mouseY, pmouseX, pmouseY }) {

    },
    mouseDragged({ mouseX, mouseY, pmouseX, pmouseY }) {
      console.log(mouseX, mouseY, pmouseX, pmouseY)
      if(mouseX < 0 || mouseX > this.width || pmouseX < 0||pmouseX > this.width | mouseY < 0 || mouseY > this.height || pmouseY < 0||pmouseY > this.height ) {
        return
      }
      this.pushLine({ mouseX, mouseY, pmouseX, pmouseY, color: 0 })
    },
    pushLine(line) {
      this.lines[this.index].push(line)
      this.$forceUpdate()
    },
    reset() {
      this.lines[this.index] = []
      this.$forceUpdate()
    },
    previous() {
      this.index -= 1
    },
    next() {
      this.index += 1
    },
    save() {

    }
  }
};
</script>
