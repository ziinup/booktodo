<template>
    <TodoHeader />
    <TodoInput v-on:addTodo="addTodo" />
    <TodoList v-bind:propsdata="todoItems" @delTodo="removeTodo"/>
    <TodoFooter v-on:removeAll="removeAll" />
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoInput from '@/components/TodoInput.vue';
import TodoList from '@/components/TodoList.vue';
import TodoFooter from '@/components/TodoFooter.vue';

export default ({
  components:{
    TodoHeader,
    TodoInput,
    TodoList,
    TodoFooter
  },
  data(){
    return {
      todoItems:[]
    }
  },
  methods:{
    addTodo(todoItem){
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeTodo(a,b){
      console.log(a ,b);
      localStorage.removeItem(a);
      this.todoItems.splice(b,1);
    },
    removeAll(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created(){
    if(localStorage.length>0){
        for(var i=0;localStorage.length>i;i++){
            this.todoItems.push(localStorage.key(i));
        }
    }
  }
})
</script>

<style>
body {text-align:center;background-color:#f6f6f8}
input {border-style: groove; width: 200px;}
button {border-style: groove;}
.shadow {box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)}
</style>
