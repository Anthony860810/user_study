<template>
  <div>
    NOW {{index}}
    <button @click="reset">Reset</button>
    <button @click="previous" v-if="index >= 1">Previous</button>
    <button @click="next">Next</button>
    <button @click="showdata">ShowData</button>
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
import file1 from './assets/1.json'
import file2 from './assets/2.json'
import file3 from './assets/3.json'
import file4 from './assets/4.json'
import file5 from './assets/5.json'
import file6 from './assets/6.json'
import file7 from './assets/7.json'
import file8 from './assets/8.json'
import file9 from './assets/9.json'
import file10 from './assets/10.json'

export default {
  name: "p5-example",
  components: {
    "vue-p5": VueP5
  },
  data: () => ({
    width: 1800,
    height: 5000,
    lines: [[], []],
    index: 0,
    original_data:file1,
    
  }),
  methods: {
    setup(sketch) {
      sketch.createCanvas(this.width, this.height)
      frameRate(120)
    },
    showdata(sketch){
      if (this.index==1){
        this.original_data = file2
      }
      else if(this.index==2){
        this.original_data = file3
      }
      else if(this.index==3){
        this.original_data = file4
      }
      else if(this.index==4){
        this.original_data = file5
      }
      else if(this.index==5){
        this.original_data = file6
      }
      else if(this.index==6){
        this.original_data = file7
      }
      else if(this.index==7){
        this.original_data = file8
      }
      else if(this.index==8){
        this.original_data = file9
      }
      else if(this.index==9){
        this.original_data = file10
      }
      else if(this.index==10){
        this.original_data = file3
      }

    },
    draw(sketch) {
      sketch.background(220, 220, 220)
      
      sketch.stroke(67,205,128)
      sketch.strokeWeight(4)
      var previous_x = 0
      var previous_y = 2500-this.original_data["0"]
      for(var idx=1 ; idx<1680 ; idx++){
        var temp = 2500-this.original_data[idx].toString()*0.5
        sketch.line(previous_x, previous_y, idx, temp)
        previous_x = idx+1
        previous_y = temp
        console.log(previous_y)
      }
      for (let line of this.lines[this.index]) {
        sketch.stroke(138,43,226)
        sketch.line(line.pmouseX, line.pmouseY, line.mouseX, line.mouseY)
      }
    },
    keyPressed({ keyCode }) {

    },
    mouseMoved({ mouseX, mouseY, pmouseX, pmouseY }) {

    },
    mouseDragged({ mouseX, mouseY, pmouseX, pmouseY }) {
      //console.log(mouseX, mouseY, pmouseX, pmouseY)
      if(mouseX < 0 || mouseX > this.width || pmouseX < 0||pmouseX > this.width | mouseY < 0 || mouseY > this.height || pmouseY < 0||pmouseY > this.height ) {
        return
      }
      this.pushLine({ mouseX, mouseY, pmouseX, pmouseY, color: (138,43,226) })
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
