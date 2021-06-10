<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    點數<input type="number" name="" v-model="n"/>
    <br/>
    間隔<input type="number" name="" v-model="d"/>
    <br/>
    <svg height="400" width="400">
      <g v-for = "(p,idx) in paths" :key="idx">
        <line :x1="p.x1" :y1="p.y1" :x2="p.x2" :y2="p.y2" :style="{stroke: color, 'stroke-width':2}" />
      </g>
      <circle v-for = "j in items" :key="j * 100 + 100" :cx="100* Math.cos(3.14 * 2 * j / items.length) + 200" :cy="100 * Math.sin(3.14 * 2 * j / items.length) + 200" r="4" stroke="black" stroke-width="3" fill="red" />
    </svg>

    <color-picker v-model="color"></color-picker>
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
      n: 10,
      d: 3,
      items: [0,1,2,3,4,5,6,7,8,9],
      paths: null
    }
  },
  methods: {
    reset() {
      let list = [];
      let pist = [];
      const l = this.n;
      for (var i = 0; i < this.n; i++) {
        list.push(i)
        let obj = {}
        obj.x1 = 100 * Math.cos(3.14 * 2 * i * this.d / l) + 200
        obj.y1 = 100 * Math.sin(3.14 * 2 * i * this.d / l) + 200
        obj.x2 = 100 * Math.cos(3.14 * 2 * (i+1) * this.d / l) + 200
        obj.y2 = 100 * Math.sin(3.14 * 2 * (i+1) * this.d / l) + 200
        pist.push(obj)
        console.log(i);
        console.log(obj);
      }
      this.items = list;
      this.paths = pist;
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
</style>
