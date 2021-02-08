<template>
  <h2>Vue实现TodoList</h2>
  <div class="todolist">
    <input type="text" v-model="todo" @keyup.enter="addData()">
    <hr>
    <h4>正在进行</h4>
    <ul>
      <template v-for="(item,index) in list" :key="index">
        <li v-if="!item.checked">
          <input type="checkbox" v-model="item.checked" @change="setTodolist()"> {{item.title}} --- 
          <button @click="deleteData(index)">删除</button>
        </li>
       
      </template>
      
    </ul>

    <h4>已经完成</h4>
    <ul>
      <template v-for="(item,index) in list" :key="index">
        <li v-if="item.checked">
          <input type="checkbox" v-model="item.checked" @change="setTodolist()"> {{item.title}} --- 
          <button @click="deleteData(index)">删除</button>
        </li>
       
      </template>
      
    </ul>
    

  </div>

</template>

<script>
export default {
  data(){
    return{
      todo:"",
      list:[]

    };
  },
  methods:{
    addData(){
      this.list.push({
        title:this.todo,
        checked:false
      });
      this.todo="";
      localStorage.setItem("todolist",JSON.stringify(this.list));

    },
    deleteData(key){
      this.list.splice(key,1);
      localStorage.setItem("todolist",JSON.stringify(this.list));
    },
    setTodolist(){
      localStorage.setItem("todolist",JSON.stringify(this.list));

    }
  },
  // 页面加载的时候触发的方法
  mounted(){
    let todolist=JSON.parse(localStorage.getItem("todolist"));
    if(todolist){
      this.list=todolist;

    }
    console.log("页面加载的时候触发的方法");
    
  }
}
</script>

<style>
h2{
  text-align: center;
}

.todolist{
  width: 500px;
  border: 1px solid #eee;
  margin: 0 auto;
  padding:20px;
  
}

.todolist h3{
    color:red;
    font-size: 40px;
  }

</style>
