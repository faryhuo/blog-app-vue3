<template>
  <div class="validate-input-container pb-3">
    <input type="text" class="form-control" :class="{'is-invalid':inputRef.error}"
     :value="inputRef.val" @blur="validateInput" @input="updateValue" v-bind="$attrs" >
    <span class="invalid-feedback" v-if="inputRef.error">{{inputRef.message}}</span>
  </div>
</template>

<script lang="ts">

import { defineComponent, onMounted, PropType, reactive } from 'vue'
import { emitter } from '../ValidationForm/ValidationForm.vue'

type ruleType='required' | 'email' | 'custom';

interface RuleProps{
    type:ruleType;
    message?:string;
    customValid?: (value:any)=> boolean;
}

export type RulesProps=RuleProps[];

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
    const getDefaultErroeMessage = (type:ruleType) => {
      switch (type) {
        case 'required':
          return 'cannot be empty'
        case 'email':
          return 'email format is incorrect'
        default:
          return ''
      }
    }

    const validateInput = () => {
      if (props.rules) {
        const allPassed = props.rules.every(rule => {
          let passed = true
          if (rule.message) {
            inputRef.message = rule.message
          } else {
            inputRef.message = getDefaultErroeMessage(rule.type)
          }
          switch (rule.type) {
            case 'required':
              passed = (inputRef.val.trim() !== '')
              break
            case 'email':
              passed = eamilReg.test(inputRef.val)
              break
            case 'custom':
              passed = rule.customValid ? rule.customValid(inputRef.val) : true
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
    onMounted(() => {
      emitter.emit('form-item-created', validateInput)
    })

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
