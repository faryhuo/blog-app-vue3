<template>
  <div class="validate-input-container pb-3">
    <input type="text" class="form-control" :class="{'is-invalid':inputRef.error}"
     :value="inputRef.val" @blur="validateInput" @input="updateValue" v-bind="$attrs" >
    <span class="invalid-feedback" v-if="inputRef.error">{{inputRef.message}}</span>
  </div>
</template>

<script lang="ts">

import { defineComponent, PropType, reactive } from 'vue'

interface RoleProps{
    type:'required' | 'email';
    message:string;
}

export type RulesProps=RoleProps[];

export default defineComponent({
  name: 'ValidationInput',
  props: {
    rules: Array as PropType<RulesProps>,
    modelValue: String
  },
  inheritAttrs: false,
  setup (props, context) {
    const inputRef = reactive({
      val: props.modelValue || '',
      error: false,
      message: ''
    })
    const eamilReg = /^[A-Za-zd0-9]+([-_.][A-Za-zd]+)*@([A-Za-zd]+[-.])+[A-Za-zd]{2,5}$/
    const updateValue = (e: KeyboardEvent) => {
      const targetValue = (e.target as HTMLInputElement).value
      inputRef.val = targetValue
      context.emit('update:modelValue', targetValue)
    }
    const validateInput = () => {
      if (props.rules) {
        const allPassed = props.rules.every(rule => {
          let passed = true
          inputRef.message = rule.message
          switch (rule.type) {
            case 'required':
              passed = (inputRef.val.trim() !== '')
              break
            case 'email':
              passed = eamilReg.test(inputRef.val)
              break
            default:
              break
          }
          return passed
        })
        inputRef.error = !allPassed
        return allPassed
      } else {
        return true
      }
    }
    return {
      inputRef,
      validateInput,
      updateValue
    }
  }
})

</script>

<style>

</style>
