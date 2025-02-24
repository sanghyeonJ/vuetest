<template>
  <main>
    <div class="container py-4">
        <div class="container text-center">
            <PostCreate @create-post="createPost"/>
            <!-- @자식컴포넌트에서 보낸 이벤트="부모컴포넌트의 메소드" -->
            <!-- 
            자식 컴포넌트에서 의 버튼에 @click="createPost" 를 추가하고, 해당 메소드에 context.emit("부모컴포넌트의 메소드", 매개변수)추가, emits에 createPost이벤트를 등록
            부모 컴포넌트에서 자식컴포넌트 태그에 @create-post="부모컴포넌트의 메소드" 를 추가
            => 자식 컴포넌트의 버튼을 누르면 부모컴포넌트의 메소드 실행
            -->

            <hr class="my-4">
            <div class="row g-4">

                <div class="col col-4" v-for="post in posts" :key="post.id">
                    <AppCard :title="post.title" :content="post.content" :type="post.type" :is-like="post.isLike" :obj="obj" @toggle-like="post.isLike = !post.isLike"  />
                    <!-- 속성명이 is-like(케밥케이스) 이면 속성값이 isLike(카멜케이스) 로 들어간다. 속성을 선언할때는 카멜케이스, 사용할때는 케밥케이스 사용을 권장 (공식문서) -->
                </div>
            </div>

            <hr class="my-4">
            
            <!-- <LabelInput :modelValue="userName" @update:modelValue="value => (userName = value)"/> -->
            <LabelInput v-model="userName" label="이름"/>
            <hr>
            <UserName v-model:firstName="firstName" v-model:lastName="lastName"/>
        </div>
    </div>
  </main>
</template>

<script>
import AppCard from './AppCard.vue'
import PostCreate from './PostCreate.vue'
import LabelInput from './LabelInput.vue'
import UserName from './UserName.vue'
import { reactive, ref } from 'vue'

export default {
  components: {
    AppCard,
    PostCreate,
    LabelInput,
    UserName
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

    const createPost = (newPost) => {
        console.log(newPost)
        posts.push(newPost)
    }

    const userName = ref('')

    const firstName = ref('')
    const lastName = ref('')
    
    return {
        obj,
        posts,
        createPost,
        userName,
        firstName,
        lastName
    }
  }
}
</script>

<style>

</style>