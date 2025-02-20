<template>
    <div>
      <div :class="{ active: isActive }">텍스트</div>  <!-- {클래스명: boolean 타입, ...} 형식으로 클래스 적용 -->
      <div :class="classObject">텍스트</div>  <!-- 객체 형식으로 여러 클래스 적용 -->
      <button @click="toggle">toggle</button>
      <button @click="toggleError">toggleError</button>
  
      <hr>
  
      <button @click="fontSize++">+</button>
      <button @click="fontSize--">-</button>
      <div :style="styleObject">Lorem ipsum dolor sit amet consectetur adipisicing elit. Qui cumque quis rem officia harum, dignissimos, quibusdam recusandae dolor illum cupiditate minima molestiae sit quo quae facere repellat voluptatum aspernatur ut!</div>
    </div>
  </template>
  
  <script>
  import { reactive, ref, computed } from 'vue';
  
  export default {
    setup(){
  
      const isActive = ref(true);
      const isError = ref(false);
  
      const toggle = () => {
          isActive.value = !isActive.value;
      }
      const toggleError = () => {
          isError.value = !isError.value;
      }
  
      // const classObject = reactive({
      //     active: isActive,
      //     error: isError
      // });
  
      const classObject = computed(() => {  // 조건이 여러개일때는 computed를 사용하여 표현
          return {
              active: true && true,
              error: isError.value
          }
      });
  
      ////////////////////////////////
      const fontSize = ref('13');
  
      // const styleObject = reactive({
      //     color: 'red',
      //     fontSize: fontSize.value + 'px' // reactive는 초기 생성시점의 값을 기억하기 때문에 값이 변경되어도 변경된 값을 기억하지 않음
      // });
  
      const styleObject = computed(() => {  // computed는 fontSize.value의 변화를 감지하고 새로운 값으로 업데이트 됨
          return {
              color: 'red',
              fontSize: fontSize.value + 'px'
          }
      })
  
      return{
        isActive,
        toggle,
        classObject,
        toggleError,
        styleObject,
        fontSize,
      }
    }
  }
  </script>
  
  <style>
  .active{
    font-weight: bold;
  }
  
  .error{
    color: red;
  }
  </style>