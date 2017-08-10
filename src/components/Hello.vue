<template>
  <div class="hello">
    <div id="gjs"></div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    var editor = grapesjs.init({
      container: '#gjs',
      components: '<div class="txt-red">Hello world!</div>',
      style: '.txt-red{color: red}'
    })
    console.log(editor)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
