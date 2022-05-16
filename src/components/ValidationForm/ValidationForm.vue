<template>
  <form class="validate-form-container pb-3">
    <slot name="default"></slot>
    <div class="submit-area">
      <slot name="submit">
        <button type="submit" @click.prevent="submitForm" class="btn btn-primary">Submit</button>
      </slot>
    </div>
 </form>
</template>

<script lang="ts">

import { defineComponent, onUnmounted, PropType, reactive } from 'vue'
import mitt from 'mitt'

export const emitter = mitt()
type ValidateFunc = () => boolean

export default defineComponent({
  name: 'ValidationForm',
  props: {
    modelValue: String
  },
  emits: ['form-submit'],
  setup (props, context) {
    let funcArr: ValidateFunc[] = []
    const submitForm = () => {
      const result = funcArr.map(func => func()).every(result => result)
      context.emit('form-submit', result)
    }
    const callback = (func: any) => {
      funcArr.push(func)
    }
    emitter.on('form-item-created', callback)
    onUnmounted(() => {
      emitter.off('form-item-created', callback)
      funcArr = []
    })

    return {
      submitForm
    }
  }
})

</script>

<style>

</style>
