<template>
    <div>
      <h3>input value</h3>
      <input type="text" :value="inputValue">  <!-- 단방향 바인딩 -->
      <input type="text" v-model="inputValue">  <!-- 양방향 바인딩 -->
      <p>{{ inputValue }}</p>
    </div>
  </template>
  
  <script>
  import { reactive, ref } from 'vue';
  
  export default {
    setup(){
  
      const inputValue = ref(null);
  
      return {
        inputValue
      }
    }
  }
  </script>
  
  <style>
  </style>