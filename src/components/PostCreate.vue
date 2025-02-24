<template>
    <div class="row g-3">
        <div class="col col-2">
            <select v-model="type" class="form-select" aria-label="Default select example">
                <option value="news">news</option>
                <option value="notice">notice</option>
            </select>
        </div>
        <div class="col col-8">
            <input type="text" class="form-control" v-model="title">
        </div>
        <div class="col col-2 d-grid">
            <!-- <button class="btn btn-primary" @click="$emit('createPost', 1, 2, 3, '김길동')">button</button> -->
            <button class="btn btn-primary" @click="createPost">추가</button>
            <!-- 자식컴포넌트에서 부모컴포넌트로 이벤트를 전달할때는 내장함수인 $emit('이벤트명') 을 사용한다. -->
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    //emits: ['createPost'],
    emits: { // 객체형태로 적용하면 이벤트 전달시 유효성 검사를 할수있다.
        createPost: (newPost) => {
            if (!newPost.type) {  // 결과값이 비어있으면 false를 반환하여 경고를 출력한다
                return false
            } else if (!newPost.title) {
                return false
            }
            return true
        }
        // imsi: null  유효성검사가 필요없는 경우 null
    },
    setup(props, context){
        // context객체안에 emit이 있는것이므로 구조분해할당을 이용해서 setup(props, {emit}) 으로 사용해도 된다.

        const title = ref('');
        const type = ref('news');


        //context.emit('createPost', 1, 2, 3, '김길동')
        const createPost = () => {
            const newPost = {
                type: type.value,
                title: title.value,
            }
            context.emit('createPost', newPost)
            // context를 구조분해할당으로 사용하면 앞의 context를 사용하지 않아도 된다. => emit('createPost', 1, 2, 3, '김길동')

            type.value = 'news'
            title.value = ''
        }
        return {
            createPost,
            title,
            type
        }
    }
}
</script>

<style>

</style>