
<template>
    <div>
      <h2>반응형 메시지</h2>
      <p>{{ reactiveMessage }}</p>
      <button v-on:click="addReactiveMessage">add</button>
      <h2>일반 메시지</h2>
      <p>{{ normalMessage }}</p>
      <button v-on:click="addNormalMessage">add</button>
    </div>
  </template>
  
  <script>
  import { ref, isRef, onMounted, onBeforeMount } from 'vue';
  
  export default {
      setup(){
          console.log('setup');
          // 반응형 메시지
          // 반응형 데이터는 값이 변함에 따라 자동으로 업데이트 된다.
          const reactiveMessage = ref('hello reactive message');
          const addReactiveMessage = () => {
              reactiveMessage.value += '!';
          }
          console.log('isRef(reactiveMessage): ', isRef(reactiveMessage));
  
          // 일반 메시지
          let normalMessage = 'hello normal message';
          const addNormalMessage = () => {
              normalMessage = normalMessage + '!';
          }
          console.log('isRef(normalMessage): ', isRef(normalMessage));
  
  
          onMounted(() => {
              console.log('onMounted');
          });
          onBeforeMount(() => {
              console.log('onBeforeMount');
          });
          
  
          // 변수나 함수등은 return에 넣어줘야 템플릿에서 사용할 수 있다.
          return {
              reactiveMessage,
              normalMessage,
              addReactiveMessage,
              addNormalMessage
          }
      }
  }
  </script>
  
  <style scoped>
  </style>
  