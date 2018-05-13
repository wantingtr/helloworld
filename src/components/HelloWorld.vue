<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button @click='onClickMe' name="button">Click!</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to the HelloWorld component'
    }
  },
  props:['msgfromfather'],
  methods:{
    onClickMe: function(){
        console.log(this.msgfromfather)
    }
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
