<template>
  <div id="app">
    <h2>Todos Again - vue.js</h2>
    <input id="app-input" v-model="newItem" @keyup.enter="addNew" placeholder="what are you diong?">
    <ul>
      <li v-for="item,index in items">
        <h3 @mouseenter="itemEnter(item)" @mouseleave="itemLeave(item)">
          <input type="checkbox" @click="itemCheck(item)">
          <p class="item-label" v-bind:class="{'line-through':item.checked}">{{index + 1}}.{{item.label}}</p>
          <p class="item-status" v-if='item.checked'>finished</p>
          <p class="item-delete" v-if='item.showDelete' @click="deleteClick(item)">Delete</p>
        </h3>
      </li>
    </ul>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Store from './store'

export default {
  data () {
    return {
      newItem:"",
      items:Store.fetch(),
    }
  },
  methods:{
    addNew:function () {
      this.items.push({
        label:this.newItem,
        checked:false,
        showDelete:false,
      });
      this.newItem = "";
    },
    itemEnter:function (item) {
      item.showDelete = true;
    },
    itemLeave:function (item) {
      item.showDelete = false;
    },
    itemCheck:function (item) {
      item.checked = !item.checked;
    },
    deleteClick:function (item) {
      let index = this.items.indexOf(item);
      this.items.splice(index,1);
    }
  },
  watch:{
    items:{
      handler (items) {
        Store.save(items);
      },
      deep:true,
    }
  }
}
</script>

<style>
body{
  font-family:Helvetica,sans-serif;
}
#app{
  width:800px;
  margin:30px auto;
}
#app-input{
  width:750px;
  height:35px;
  padding:0 5px;
}
ul{
  list-style:none;
  padding:0;
}
li{
  height:30px;
}
.item-label{
  display:inline;
}
.item-status{
  display:inline;
  background:red;
  color:white;
  padding:0 5px;
  font-size:12px;
}
.item-delete{
  display:inline;
  text-decoration:underline;
  font-size:12px;
  color:gray;
  cursor:pointer;
}
.line-through{
  text-decoration:line-through;
}
</style>
