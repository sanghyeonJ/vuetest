<template>
    <div>
      <ul>
          <li v-for="(item, index) in items" :key="item.id">
              {{ index }}, {{ item.message }}
          </li>
      </ul>
      <hr>
      <ul>
          <template v-for="item in items" :key="item.id">
              <li v-if="item.id % 2 === 0">
                  짝수 index : {{ item.id }}, {{ item.message }}
              </li>
          </template>
      </ul>
      <hr>
      <ul>
          <li v-for="item in evenItems" :key="item.id">
              {{ item.id }}, {{ item.message }}
          </li>
      </ul>
      <hr>
      <ul>
          <li v-for="(value, key, index) in myObject" :key="key">
              {{ index }} - {{ key }} - {{ value }}
          </li>
      </ul>
    </div>
  </template>
  
  <script>
  import { computed, reactive, ref } from 'vue';
  export default {
    setup(){
  
      const items = reactive([
          { id: 1, message: 'java' },
          { id: 2, message: 'html' },
          { id: 3, message: 'css' },
          { id: 4, message: 'javascript' },
      ])
  
      const evenItems = computed(() => {
          return items.filter(item => item.id % 2 === 0);
      });
  
      const myObject = reactive({
          title: '제목',
          author: '홍길동',
          published: '2025-01-01',
      })
  
      return {
          items,
          evenItems,
          myObject
      }
    }
  }
  </script>
  
  <style>
  
  </style>