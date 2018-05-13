<template>
  <div id="app">
    <h2>todo list</h2>
    <input id='add-input' v-model='newItem' @keyup.enter='addNew' placeholder="do what?">
    <ul>
      <li v-for='item in items'>
        <h3 @mouseenter='itemEnter(item)' @mouseleave='itemLeave(item)'>
          <input type="checkbox" @click='itemCheck(item)'>
          <p class="item-label" :class="{'line-through':!item.checked}">{{ $index + 1}} . {{ item.label }}</p>
          <p class="item-status" v-if='!item.checked'>finished</p>
          <p class="item-delete" v-if='item.showDelete' @click='deleteClick(item)'>delete</p>
        </h3>
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store.js'
import HelloWorld from './components/HelloWorld'
export default {
  data: function(){
    return{
      title:'it is a todolist',
      items:Store.fetch(),
      newItem:''
    }
  },
  methods:{
    addNew:function(){
      this.items.push({
        label:this.newItem,
        checked:false,
        showDelete:true
      })
      this.newItem=''
      Store.save()
    },
    itemCheck(item){
      item.checked=!item.checked
    },
    itemEnter(item){
      item.showDelete = true
    },
    itemLeave(item){
      item.showDelete = false
    },
    deleteClick(item){
      this.items.$remove(item)
    }
  },
  watch:{
    items: {
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.add-input{
  width: 750px;
  height:35px;
  paading: 0 5px;
}
ul{
  list-style: none;
  padding: 0;
}
li{
  height: 30px;
}
.item-status{
  display: inline;
  background:red;
  color:white;
  padding : 0 5px;
  cursor: pointer;
}
.item-delete{
  display: inline;
  text-decoration: underline;
  font-size:12px;
  color:gray;
  cursor: pointer;
}
.item-label{
  display: inline;
}
.line-through{
  text-decoration: line-through;
}
</style>
