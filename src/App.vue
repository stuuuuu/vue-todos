<script setup>
import { RouterLink, RouterView } from 'vue-router';
import "./assets/styles.scss";
import TodoHeader from './components/TodoHeader.vue';
</script>

<template>

  <TodoHeader/>
  <RouterView />
</template>
