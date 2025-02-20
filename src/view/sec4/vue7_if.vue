<template>
    <div>
      <h3 v-if="visible">hello</h3>
      <h3 v-else>bye</h3>
      <button @click="visible = !visible">toggle</button>
  
      <hr>
  
      <h2 v-if="type === 'a'">a</h2>
      <h2 v-else-if="type === 'b'">b</h2>
      <h2 v-else-if="type === 'c'">c</h2>
      <h2 v-else>d</h2>
  
      <button @click="type = 'a'">a</button>
      <button @click="type = 'b'">b</button>
      <button @click="type = 'c'">c</button>
      <button @click="type = 'd'">d</button>
  
      <hr>
  
      <h2 v-show="visible">hello</h2>  <!-- false일 경우 렌더링은 되어있지만 display: none 처리  ( if문은 렌더링 자체를 무시 ) -->
      <button @click="visible = !visible">toggle</button>
  
      <!-- 따라서 dom을 제거하고 생성하는 if는 전환비용이 높다 -->
      <!-- show의 경우에는 초기 렌더링 비용이 높다 -->
      <!-- 자주 전환해야하는 경우에는 show를 사용하고, 전환이 적은 경우(조건이 변하지 않는 경우)에는 if를 사용하는 것이 좋다 -->
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
    setup(){
  
      const visible = ref(true);
      const type = ref('a');
  
      return {
        visible,
        type
      }
    }
  }
  </script>
  
  <style>
  
  </style>