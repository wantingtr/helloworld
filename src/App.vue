<template>
  <div id="app">
    <h2 >A Vue.js Demo - To Do List</h2>
    <h2 class='c1'>by wantingtr</h2>
    <input id='add-input' v-model='newItem' @keyup.enter='addNew' placeholder="do what?">
    <ul>
      <li v-for='(item,index) in items'>
        <h3 @mouseenter='itemEnter(item)' @mouseleave='itemLeave(item)'>
          <p class="item-label" :class="{'line-through':item.checked}">{{ index+1 }} . {{ item.label }}</p>
          <label class='item-status' v-if='!item.checked' @click='item.checked=true'>Finished</label>
          <p class="item-delete" v-if='item.showDelete' @click='deleteClick(index)'>delete</p>
        </h3>
      </li>
    </ul>
    <button class='delete-button' type="button" name="deleteall" @click='deleteall()'>Delete all</button>
  </div>
</template>

<script>
import Store from './store.js'
export default {
  data: function(){
    return{
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
    },
    itemEnter(item){
      item.showDelete = true
    },
    itemLeave(item){
      item.showDelete = false
    },
    deleteClick(index){
      this.items.splice(index, 1)
    },
    deleteall(){
      this.items = [];
    }
  },
  watch:{
    items: {
      handler:function(items){
        Store.save(items)
      },
      deep: true
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  text-align: center;
}
.c1{
  font-size: 15px;
}
.add-input{
  width: 750px;
  height:35px;
  paading: 0 5px;
}
.item-status{
  display: inline;
  background:red;
  color:white;
  padding : 0 5px;
  cursor: pointer;
}
ul{
  margin: 0px;
  padding: 0px;
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
.delete-button{
  margin:20px;
}
</style>
