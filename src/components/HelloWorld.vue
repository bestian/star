<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    點數<input type="number" name="" v-model="n"/>
    <br/>
    間隔<input type="number" name="" v-model="d"/>
    <br/>
    間隔2<input type="number" name="" v-model="d2"/>
    <br/>
    <button @click="saveSvg()">存檔!</button>
    <br/>
    <svg height="400" width="400" id = "star">
      <g v-for = "(p,idx) in paths" :key="idx">
        <line :x1="p.x1" :y1="p.y1" :x2="p.x2" :y2="p.y2" :style="{stroke: color, 'stroke-width':2}" />
      </g>
      <g v-for = "(p,idx) in paths2" :key="idx">
        <line :x1="p.x1" :y1="p.y1" :x2="p.x2" :y2="p.y2" :style="{stroke: color2, 'stroke-width':2}" />
      </g>
      <circle v-for = "j in items" :key="j * 100 + 100" :cx="100* Math.cos(3.14 * 2 * j / items.length) + 200" :cy="100 * Math.sin(3.14 * 2 * j / items.length) + 200" r="4" stroke="black" stroke-width="3" fill="red" />
    </svg>
    <hr/>
    <color-picker v-model="color"></color-picker>
    <color-picker v-model="color2"></color-picker>
  </div>
</template>

<script>

import ColorPicker from 'vue-color-picker-wheel';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: {
      ColorPicker
  },
  data() {
    return {
      color: '#0f0',
      color2: '#00f',
      n: 10,
      d: 3,
      d2: 2,
      items: [0,1,2,3,4,5,6,7,8,9],
      paths: null,
      paths2: null
    }
  },
  methods: {
    saveSvg() {
      let svgEl = document.getElementById('star')
      svgEl.setAttribute("xmlns", "http://www.w3.org/2000/svg");
      var svgData = svgEl.outerHTML;
      var preface = '<?xml version="1.0" standalone="no"?>\r\n';
      var svgBlob = new Blob([preface, svgData], {type:"image/svg+xml;charset=utf-8"});
      var svgUrl = URL.createObjectURL(svgBlob);
      var downloadLink = document.createElement("a");
      downloadLink.href = svgUrl;
      downloadLink.download = 'star';
      document.body.appendChild(downloadLink);
      downloadLink.click();
      document.body.removeChild(downloadLink);
    },
    reset() {
      let list = [];
      let pist = [];
      let pist2 = [];
      const l = this.n;
      for (var i = 0; i < this.n; i++) {
        list.push(i)
        let obj = {}
        obj.x1 = 100 * Math.cos(3.14 * 2 * i * this.d / l) + 200
        obj.y1 = 100 * Math.sin(3.14 * 2 * i * this.d / l) + 200
        obj.x2 = 100 * Math.cos(3.14 * 2 * (i+1) * this.d / l) + 200
        obj.y2 = 100 * Math.sin(3.14 * 2 * (i+1) * this.d / l) + 200
        let obj2 = {}
        obj2.x1 = 100 * Math.cos(3.14 * 2 * i * this.d2 / l) + 200
        obj2.y1 = 100 * Math.sin(3.14 * 2 * i * this.d2 / l) + 200
        obj2.x2 = 100 * Math.cos(3.14 * 2 * (i+1) * this.d2 / l) + 200
        obj2.y2 = 100 * Math.sin(3.14 * 2 * (i+1) * this.d2 / l) + 200
        pist.push(obj);
        pist2.push(obj2);
        console.log(i);
        console.log(obj);
      }
      this.items = list;
      this.paths = pist;
      this.paths2 = pist2;
      console.log(pist);
      this.$forceUpdate;
    },
  },
  watch: {
    n(){
      this.reset()
    },
    d() {
      this.reset()
    },
    d2() {
      this.reset()
    }
  },
  mounted() {
    this.reset()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
input {
  margin-left: 1.6em;
  font-size: 18px;
}
</style>
