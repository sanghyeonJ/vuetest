<template>
    <main>
        <div class="container py-4">
            <MyButton class="buttonClass" id="buttonId" @click="sayHello"/>
            <!-- 현재 버튼 컴포넌트 내에는 props가 없다 ( 클릭 이벤트가 없음 ) -->
            <!-- non props 속성은 부모컴포넌트에서 상속된다 -->

            <LabelInput label="이름" data-id="inputId"></LabelInput>
        </div>
    </main>
</template>

<script>
import MyButton from './MyButton.vue'
import LabelInput from './LabelInput.vue'
export default {
    components: {
        MyButton,
        LabelInput
    },

    setup(){

        const sayHello = () => {
            alert('hello')
        }
        

        return {
            sayHello
        }
    }
}
</script>

<style>

</style>