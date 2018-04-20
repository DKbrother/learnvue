<template>
  <div class="hello">
    <h1>{{title}}</h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :={finished:item.isFinished} @click="toggleFinish(item)">
        {{item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      title:"This is a todo-list",
      items:[
        {label:"coding",isFinished:false},
        {label:"walking",isFinished:true},
      ],
      newItem:"",
    }
  },
  methods:{
    toggleFinish:function (item) {
      item.isFinished = !item.isFinished;
    },
    addNew:function ()　{
      this.items.push({
        label:this.newItem,
        isFinished:false,
      })
      this.newItem = "";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
