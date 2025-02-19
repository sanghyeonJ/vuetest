<template>
    <div>
      <h2>{{ teacher.name }}</h2>
      <h3>강의가 있습니까?</h3>
      <p>{{ teacher.lecture.length > 0 ? '있습니다.' : '없습니다.' }}</p>
      <p>{{ hasLecture }}</p>
      <p>{{ hasLecture }}</p>
      <p>{{ existLecture() }}</p>
      <p>{{ existLecture() }}</p>
  
      <button @click="counter++">{{ counter }}</button>
  
      <hr>
  
      <p>{{ fullName }}</p>
    </div>
  </template>
  
  <script>
  import { computed, reactive, ref } from 'vue';
  
  export default {
      setup(){
          const teacher = reactive({
              name: '홍길동',
              lecture: ['vue', 'react', 'node']
          });
  
          const hasLecture = computed(() => {
              console.log('computed 호출');
              return teacher.lecture.length > 0 ? '있습니다.' : '없습니다.' 
          });
  
          const existLecture = () => {
              console.log('method 호출');
              return teacher.lecture.length > 0 ? '있습니다.' : '없습니다.' 
          };
          // computed는 캐시되어 있어 첫번째 호출 후 값이 변경되지 않으면 캐시된 값을 반환한다 => 성능에서 유리
  
          const counter = ref(0);
  
  
          const firstName = ref('홍');
          const lastName = ref('길동');
  
          const fullName = computed(() => {
              return firstName.value + ' ' + lastName.value;
          });
          fullName.value = '임 꺽정';  // readonly 이기 때문에 변경 불가
          console.log('fullName: ' + fullName.value);
  
          // 변경을 위해서는 get(), set() 메서드를 사용해야 한다
          const fullNameChange = computed({
              get(){
                  return firstName.value + ' ' + lastName.value;
              },
              set(value){
                  console.log('set():' + value);
                  [firstName.value, lastName.value] = value.split(' ');
                  console.log('first: ' + firstName.value);
                  console.log('last: ' + lastName.value);
              }
          });
          fullNameChange.value = '임 꺽정';
          console.log('fullNameChange: ' + fullNameChange.value);
  
          return{
              teacher,
              hasLecture,
              existLecture,
              counter,
              firstName,
              lastName,
              fullName,
              fullNameChange
          }
      }
  }
  </script>
  
  <style>
  
  </style>