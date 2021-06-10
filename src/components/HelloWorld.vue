<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <svg height="400" width="400">
      <circle v-for = "i in [0,1,2,3,4,5,6,7,8,9]" :key="i" :cx="100* Math.cos(3.14 * i / 5) + 200" :cy="100 * Math.sin(3.14 * i / 5) + 200" r="4" stroke="black" stroke-width="3" fill="red" />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
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
