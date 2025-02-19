
<template>
    <div>
      <h2>보간법</h2>
      <p>{{ message }}</p>
      <p v-once>{{ message }}</p>
      <!-- v-once 디렉티브는 데이터가 갱신되지않는 일회성 보간 -->
      <button @click="message = message + '!'">click</button>
  
      <hr>
      
      <h2>HTML 보간법</h2>
      <p>{{ rawHtml }}</p> <!-- 문자열 그대로 보여줌 -->
      <p v-html="rawHtml"></p> <!-- HTML 태그 형식으로 보여줌 -->
      <button @click="rawHtml = rawHtml + '!'">click</button>
      
      <hr>
  
      <h2>속성 바인딩</h2>
      <div title="일반 타이틀속성">mouse over</div> <!-- title속성은 툴팁을 보여주는 속성 -->
      <div v-bind:title="dynamicTitle">mouse over</div> <!-- v-bind:title="dynamicTitle"는 title속성을 dynamicTitle변수의 값으로 바인딩 -->
      <input type="text" value="홍길동" v-bind:disabled="isInputDisabled" /> <!-- boolean 타입도 추가할수있다 -->
      <input v-bind="attrs" /> <!-- 객체 타입도 추가할수있다 -->
      
      <h2>javascript 표현식</h2>
      <p>{{ message.split('').reverse().join('') }}</p> <!-- 문자열 뒤집기 -->
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
      setup(){
          const message = ref('hello');
          const rawHtml = ref('<span>This is html</span>');
  
          const dynamicTitle = ref('반응형 타이틀속성');
          const isInputDisabled = ref(true);
          const attrs = ref({
              type: 'password',
              placeholder: '비밀번호를 입력하세요',
              value: '123456789'
          })
          
          return {
              message,
              rawHtml,
              dynamicTitle,
              isInputDisabled,
              attrs
          }
      }
  }
  </script>
  
  <style scoped>
  </style>
  