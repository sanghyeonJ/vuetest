<template>
  <main>
    <div class="container py-4">
        <div class="container text-center">
            <PostCreate @create-post="createPost"/>
            <div class="row g-4">

                <div class="col col-4" v-for="post in posts" :key="post.id">
                    <AppCard :title="post.title" :content="post.content" :type="post.type" :is-like="post.isLike" :obj="obj" @toggle-like="post.isLike = !post.isLike"  />
                    <!-- 속성명이 is-like(케밥케이스) 이면 속성값이 isLike(카멜케이스) 로 들어간다. 속성을 선언할때는 카멜케이스, 사용할때는 케밥케이스 사용을 권장 (공식문서) -->
                </div>
            </div>
        </div>
    </div>
  </main>
</template>

<script>
import AppCard from './AppCard.vue'
import PostCreate from './PostCreate.vue'
import { reactive } from 'vue'

export default {
  components: {
    AppCard,
    PostCreate
  },
  setup(){
    const obj = reactive({
        title: '제목2',
        content: '내용2',
    })
    const posts = reactive([
        {
            id: 1,
            title: '제목1',
            content: '내용1',
            isLike: true,
            type: 'news',
        },
        {
            id: 2,
            title: '제목2',
            content: '내용2',
            isLike: false,
            type: 'notice',
        },
        {
            id: 3,
            title: '제목3',
            content: '내용3',
            isLike: true,
            type: 'news',
        },
        {
            id: 4,
            title: '제목4',
            content: '내용4',
            isLike: false,
            type: 'notice',
        },
        {
            id: 5,
            title: '제목5',
            content: '내용5',
            isLike: true,
            type: 'news',
        },
    ])

    const createPost = (newTitle) => {
        console.log(newTitle)
    }
    return {
        obj,
        posts,
        createPost
    }
  }
}
</script>

<style>

</style>