<template>
    <div>
      <p>{{ msg }}</p>
      <p v-text="msg"></p>
  
      <p v-text="htmlStr"></p>  <!-- 태그를 문자열로 출력 -->
      <p v-html="htmlStr"></p>
  
      <hr>
  
      <div v-memo="[subscribe]">  <!-- 배열내의 값이 변경될때만 리렌더링 -->
          <p>구독자: {{ subscribe }}</p>
          <p>조회수: {{ views }}</p>
          <p>좋아요: {{ likes }}</p>
      </div>
      <button @click="subscribe++">subs ++</button>
      <button @click="views++">views ++</button>
      <button @click="likes++">likes ++</button>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  export default {
    setup(){
  
      const msg = ref('안녕하세요');
      const htmlStr = ref('<strong>hi html</strong>');
  
  
      const subscribe = ref(4000);
      const views = ref(200);
      const likes = ref(100);
  
      return {
        msg,
        htmlStr,
        subscribe,
        views,
        likes
      }
    }
  }
  </script>
  
  <style>
  
  </style>