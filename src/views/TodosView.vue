<script setup>
import { ref, reactive } from 'vue';
import { uid } from "uid";
import { Icon } from '@iconify/vue';
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from '../components/TodoItem.vue';


const todoList = reactive([]);
const createTodo = (todo) => {
  todoList.push({
    id: uid(),
    todo,
    isCompleted: null,
    isEditing: null
  })
  
}

const toggleTodoComplete = (todoPos) =>{
todoList[todoPos].isCompleted = !todoList[todoPos].isCompleted;
}

const toggleTodoEdit = (todoPos) => {
  todoList[todoPos].isEditing = !todoList[todoPos].isEditing; 
}

const toggleTodoNewUpdate = (newTodoValue, todoPos) => {
  todoList[todoPos].todo = newTodoValue;
}


</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create-todo="createTodo" />
    <ul class="todo-list" v-if="todoList.length > 0">
      <TodoItem v-for="(todo, index) in todoList" :todo="todo" :index="index" @toggle-edit="toggleTodoEdit" @toggle-complete="toggleTodoComplete" @new-update="toggleTodoNewUpdate"/>
    </ul>
    <p class="todos-msg" v-else>
      <Icon icon="noto-v1:sad-but-relieved-face" />
      <span>You have no todos to complete! Add one!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>