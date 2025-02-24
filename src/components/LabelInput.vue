<template>
    <label>
        {{ label }}
    </label>
    <!-- <input type="text" :value="username" @input="event => (username = event.target.value)"> -->
    <!-- 
    v-model은 내부적으로 value라는 props로 값을 전달하고,
    @input 이벤트로 이벤트를 전달받음
    따라서 위의 내용을 함축하고 있음
    -->

    
    <input type="text" :value="modelValue" @input="event => $emit('update:modelValue', event.target.value)" v-bind="$attrs">
    <!-- v-bind="$attrs" 는 부모컴포넌트에서 상속받은 속성을 자식컴포넌트에 전달하는 문법이다. -->


    <!-- <input type="text" v-model="modelValue" /> -->
    <!-- 
        위와같이 할 경우 computed를 거치므로 한단계 지연됨
    -->


    <!-- label과 input 두개의 루트를 가지고있는 다중루트 컴포넌트는 vue3에서만 사용가능 -->
    <!-- 다중루트 컴포넌트에서 non props속성을 전달하기위해서는 명시적으로 전달해주어야한다 -->
</template>

<script>
import { computed } from 'vue';

export default {
    props: ['modelValue', 'label'],
    emits: ['update:modelValue'],


    setup(props, { emit }){
        const modelValue = computed({
            get(){
                return props.modelValue
            },
            set(value){
                emit('update:modelValue', value)
            }
        });
        return {
            modelValue
        }
    }
}
</script>

<style>

</style>