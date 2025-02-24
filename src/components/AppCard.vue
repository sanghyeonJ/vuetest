<template>
    <div class="card">
        <div class="card-body">
            <span class="badge text-bg-secondary">{{ typeName }}</span>
            <h5 class="card-title mt-2">{{ title }}</h5>
            <p class="card-text">{{ content }}</p>
            <a href="#" :class="isLikeClass" class="btn" @click="toggleLike">like</a>
        </div>
    </div>
</template>

<script>
import { computed } from 'vue'
export default {
    props: {
        type: {
            type: String,
            default: 'news',
            validator: (value) => {  // 유효성 검사
                return ['news', 'notice'].includes(value)  // news 또는 notice
            }
        },
        title: {
            type: String,
            required: true,  // 필수값 여부
        },
        content: {
            type: String,
            //required: true,
        },
        isLike: {
            type: Boolean,
            default: false,
        },
        obj: {
            type: Object,
            default: () => ({})
        }
    },
    emits: ['toggleLike'], // 이벤트 선언

    setup(props, context){
        // setup함수의 첫번째 매개변수는 props
        // 두번째 매개변수는 context객체
        // context안에는 emit이라는 메서드가 있다
        //console.log(props)

        const isLikeClass = computed(() => props.isLike ? 'btn-danger' : 'btn-outline-danger');
        const typeName = computed(() => props.type === 'news' ? '뉴스' : '공지사항');

        const toggleLike = () => {
            //props.isLike = !props.isLike  // 부모컴포넌트의 데이터를 변경할수없다
            // 자식컴포넌트에서 부모컴포넌트로 이벤트를 전달할때는 context.emit('이벤트명', 전달할 데이터) 를 사용한다.
            context.emit('toggleLike');
        }

        return {
            isLikeClass,
            typeName,
            toggleLike
        }
    }
}
</script>

<style>

</style>