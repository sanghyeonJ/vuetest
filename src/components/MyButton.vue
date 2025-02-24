<template>
    <div>
        <button class="btn btn-primary" v-bind="$attrs">my btn</button>
        <!-- v-bind="$attrs" 는 부모컴포넌트에서 상속받은 속성을 자식컴포넌트에 전달하는 문법이다. -->
    </div>
</template>

<script>
export default {
    inheritAttrs: false,
    setup(props, context) {
        // inheritAttrs: false, 설정된 경우 부모컴포넌트에서 상속된 속성이 자식컴포넌트에 전달되지 않는다.
        // 그럴때 상속받은 속성은 context.attrs 에 저장된다.
        console.log(context.attrs)

        return {

        }
    }
}
</script>

<style>

</style>