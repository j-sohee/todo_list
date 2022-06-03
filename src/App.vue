<template>
  <div id="app">
      <TodoHeader></TodoHeader>
      <TodoInput v-on:addTodo="addTodo"></TodoInput>
      <TodoList v-bind:propsdata="todoItems" v-on:removeTodo="removeTodo"></TodoList>
      <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data(){
    return{
      todoItems : []
    }
  },
  created(){
        if(localStorage.length > 0){
            for(var i = 0; i < localStorage.length; i++){
                this.todoItems.push(localStorage.key(i));
            }
        }
    },
  methods : {
    addTodo(todoItem){
        //로켈스토리지에 데이터를 추가하는 로직
        localStorage.setItem(todoItem, todoItem);
        this.todoItems.push(todoItem);
    },
    removeTodo(todoItem, index){
        localStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
    },
    clearAll(){
        //로컬스토리지 전체 삭제, todoItems 초기화
        localStorage.clear();
        this.todoItems = [];
    }
  },
  components: {
    'TodoHeader':TodoHeader,
    'TodoInput':TodoInput,
    'TodoList':TodoList,
    'TodoFooter':TodoFooter
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Itim&display=swap');
html,body{
 font-family: 'Itim', cursive;
}
#app{
  font-family: 'Itim', cursive;
}
body{
  text-align:center;
  background-color:#F6F6F6;
}
input{
  border-style:groove;
  width:200px;
}
button{
  border-style:groove;
}
.sahdow{
  box-shadow: 5px 10px 10px rgba(0,0,0,.03);
}
</style>
