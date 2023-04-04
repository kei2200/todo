<script setup>
  import {ref} from 'vue';
 
  const todoRef = ref('');
  const todoListRef = ref([]);
  const addTodo = () =>{
    const id = new Date().getTime;

    todoListRef.value.push({
      id: id,
      task: todoRef.value
    })

    localStorage.todoList = JSON.stringify(todoListRef.value);
    todoRef.value ='';
  }
</script>

<template>
  <div class="box__input">
    <input type="text" class="todo__input" v-model="todoRef" placeholder="+TODOを入力">
    <button class="btn" @click="addTodo">追加</button>
  </div>
</template>

<style scoped>
    .box__input {
        margin-top: 20px;
        display: flex;
    }
    .todo__input{
        width: 300px;
        margin-right: 8px;
        padding: 8px;
        font-size: 18px;
        border: 1px solid #aaa;
        border-radius: 6px;
    }
    .btn{
        padding: 8px;
        background-color: #03a9f4;
        border-radius: 6px;
        color: #fff;
        text-align: center;
        font-size: 14px;
        white-space: nowrap;
        border: none;
    }
</style>
