<template>
    <div>
      
    </div>
  </template>
  
  <script>
  import { reactive, ref, watch } from 'vue';
  
  export default {
    setup(){
  
      const message = ref('');
      watch(message, (newMessage, oldMessage) => {
          console.log(newMessage, oldMessage);
      });
      // 첫번째 인자는 감시할 대상을 지정,
      // 두번째 인자는 콜백함수로 새로운 값과 이전 값을 매개변수로 받음
  
  
      const x = ref(0)
      const y = ref(0)
  
      // 첫번째 매개변수는 함수가 될수도 있음 ( 배열, 객체 또한 가능 )
      // 단 객체 내부의 하나의 값에 대해서만 감시를 하기 위해서는 getter함수로 사용
      const obj = reactive({
          count: 0
      })
      // watch(obj.count, (newObj, oldObj)=>{
      //     console.log(newObj, oldObj);
      // })
      // 위 대신 아래 사용
      watch(()=>obj.count, (newCount, oldCount)=>{
          console.log(newCount, oldCount);
      })
      // 리턴하는 값에 변화가 생기면 두번째 콜백함수가 실행됨
      watch(() => {
          return x.value + y.value
      }, (sum)=>{
          console.log('sum : ', sum);
      })
  
      watch([x, y], ([newX, newY], [oldX, oldY]) => {
          console.log(newX, newY, oldX, oldY);
      })
  
      return {
          message,
          x,
          y,
          obj
      }
    }
  }
  </script>
  
  <style>
  </style>