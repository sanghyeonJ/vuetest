<template>
    <div>
      <button @click="printEventInfo('hello', $event)">inline event handler</button>
      <input type="text" @keyup="keyupHandler">
  
      <hr>
  
      <div id="modifier">
        <div @click="clickDiv">
          div 영역
          <p @click="clickP">
              p 영역
              <span @click.stop="clickSpan">span 영역</span>
          </p>
        </div>
      </div>
  
      <hr>
  
      <input type="text" @keyup.enter="addTodo">
      <ul>
          <li v-for="(todo, index) in todos" :key="index">{{ todo }}</li>
      </ul>
  
    </div>
  </template>
  
  <script>
  import { reactive } from 'vue';
  
  export default {
    setup(){
  
      const printEventInfo = (message, event) => {
          console.log('message : ', message);
          console.log('event.target : ', event.target);
          console.log('event.target.tagName : ', event.target.tagName);
      }
  
      const keyupHandler = (event) => {
          console.log('event.key : ', event.key);
      }
      const clickDiv = () => {
          console.log('clickDiv');
      }
      const clickP = () => {
          console.log('clickP');
      }
      const clickSpan = (e) => {
          console.log('clickSpan');
          // e.stopPropagation(); // 이벤트 전파 방지
          // stopPropagation이 없어도 클릭요소에 @click.stop 추가시 버블링 방지
      }
      // span 클릭시 span > p > div 순으로 클릭됨 (버블링)
      // 버블링 : 이벤트가 발생한 요소에서 이벤트가 일어나면 상위 요소로 전파되는 현상
      // 캡쳐링 : 이벤트가 발생한 요소에서 이벤트가 일어나면 하위 요소로 전파되는 현상
  
  
      ////////////////////////////
  
      const todos = reactive([]);
      const addTodo = (event) => {
          // if(event.key === 'Enter'){
          //     todos.push(event.target.value);
          //     event.target.value = '';
          // }
          // 위 코드 대신 @keyup.enter 이벤트 사용
          todos.push(event.target.value);
          event.target.value = '';
      }
  
      return {
        printEventInfo,
        keyupHandler,
        clickDiv,
        clickP,
        clickSpan,
        todos,
        addTodo
      }
    }
  }
  </script>
  
  <style>
  #modifier div,
  #modifier p,
  #modifier span {
      padding: 20px;
  }
  
  #modifier div {
      background-color: #ccc;
  }
  
  #modifier p {
      background-color: #999;
  }
  
  #modifier span {
      background-color: #666;
      display: block;
  }
  </style>