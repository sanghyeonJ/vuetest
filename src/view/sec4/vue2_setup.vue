
<template>
    <div>
      <b>{{ counter }}</b>
      <button @click="addCounter">add</button>
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
      // setup 함수에서 return 하는 데이터는 템플릿에서 사용할 수 있다.
      // setup 함수의 첫번째 매개변수로는 props가 들어온다.
      // setup 함수의 두번째 매개변수로는 context가 들어온다. (속성을 가지고 있다.)
      setup(props, context){
          const counter = ref(0);
          const message = ref('hello');
          
          const addCounter = () => {
              counter.value++;
          }
  
          return {
              counter,
              message,
              addCounter
          }
      }
  }
  </script>
  
  <style scoped>
  </style>
  