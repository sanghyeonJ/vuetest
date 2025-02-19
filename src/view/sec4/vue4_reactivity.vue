<template>
    <div>
      <p>count: {{ state.count }}</p>
      <button v-on:click="increment">{{ state.count }}</button>
      <p>deep.count: {{ state.deep.count }}</p>
      <button v-on:click="incrementDeep">{{ state.deep.count }}</button>
  
      <hr>
  
      <p>message: {{ message }}</p>
      <button v-on:click="addMessage">Change Message</button>
  
      <hr>
  
      <p>messageObj: {{ messageObj.value }}</p>
      <button v-on:click="addMessageObj">Change Message</button>
  
      <hr>
  
      <p>messageRef: {{ messageRef }}</p>
      <button v-on:click="addMessageRef">Change Message</button>
  
      <hr><hr>
  
      <p>author: {{ author }}</p>
      <p>title: {{ title }}</p>
    </div>
  </template>
  
  <script>
  import { reactive, ref, toRefs, toRef, readonly } from 'vue';
  
  export default {
      // 반응형 상태를 생성하기 위해서는 reactive() 함수를 사용한다.
      // 반환된 상태는 반응형 객체이다.
      setup(){
          const state = reactive({
              count: 0,
              deep: {
                  count: 0
              }
          });
  
          const increment = () => state.count++;
          const incrementDeep = () => state.deep.count++;
  
          ////////////////////////
  
          // reactive() 함수는 객체나 배열을 반응형 객체로 변환하는 함수이다.
          // 따라서 문자열, 숫자, 불리언 등의 기본 타입은 reactive() 함수를 사용할 수 없다.
          let message = reactive('Hello, Vue!');
          const addMessage = () => message += '!';
  
          // 이런 문제를 해결하고자 객체형태로 만들어준다
          const messageObj = reactive({
              value: 'Hello, Vue!'
          })
          const addMessageObj = () => messageObj.value += '!';
  
          // 이런 형태를 간단히 사용할수있는 ref() 함수를 사용한다
          // ref함수는 value라는 하나의 속성만 가지는 객체를 반환한다
          const messageRef = ref('Hello, Vue!');
          const addMessageRef = () => messageRef.value += '!';
  
  
          /////////////////////
          // ref => object
          // ref로 선언한 데이터를 반응형 객체의 속성으로 사용하면 자동으로 unwrapping 된다
          const count = ref(0);
          const countState = reactive({
              count
          });
          console.log(count.value);
          console.log(countState.count);  // 자동으로 unwrapping 되기 때문에 value를 붙이지 않아도 된다
  
          // ref => array
          const messageArr = ref('hello');
          const arr = reactive([messageArr]);
          console.log(arr[0].value);  // 배열에서 사용하면 value를 붙여야 한다
  
          // 구조분해할당
          const book = reactive({
              author: 'evan you',
              year: '2016',
              title: 'vue.js guide',
              description: 'vue.js 가이드',
              price: 10000
          });
          // 구조분해할당을 하면 반응성을 잃고 일반 변수가 된다.
          // const { author, title } = book;
  
          // 이를 해결하기 위해 toRefs, toRef 함수를 사용한다
          //const { author, title } = toRefs(book);  // 한번에 여러개 할당
          const author = toRef(book, 'author');
          const title = toRef(book, 'title');
  
  
          /////////////////////////////
          // readonly
          const original = reactive({
              count: 0
          });
          const copy = readonly(original);
          original.count++;
          copy.count++;  // copy는 readonly이기 때문에 증가되지 않는다
          console.log('original.count: ' + original.count);
          console.log('copy.count: ' + copy.count);
  
          
          return{
              state,
              increment,
              incrementDeep,
              message,
              addMessage,
              messageObj,
              addMessageObj,
              messageRef,
              addMessageRef,
              count,
              countState,
              author,
              title
          }
      }
  }
  </script>
  
  <style>
  
  </style>