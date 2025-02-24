<template>
  <div>
    <LableInput label="성" :modelValue="firstName" @update:model-value="value => $emit('update:firstName', value)"></LableInput>
    <LableInput label="이름" :modelValue="lastName" @update:model-value="value => $emit('update:lastName', value)"></LableInput>
  </div>
</template>

<script>
import LableInput from './LabelInput.vue'
import { ref } from 'vue'
export default {
  props: ['firstName', 'lastName'],
  emits: ['update:firstName', 'update:lastName'],
  components: {
    LableInput
  },
  setup(){
    const firstName = ref('')
    const lastName = ref('')

    return {
      firstName,
      lastName
    }
    
  }
}
</script>

<style>

</style>