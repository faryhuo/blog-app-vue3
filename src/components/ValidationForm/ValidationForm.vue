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

import { defineComponent, PropType, reactive } from 'vue'

export default defineComponent({
  name: 'ValidationForm',
  props: {
    modelValue: String
  },
  emits: ['form-submit'],
  setup (props, context) {
    const submitForm = () => {
      context.emit('form-submit', true)
    }
    return {
      submitForm
    }
  },
  mounted () {
    this.$on('item-created', () => {
      //
    })
  }
})

</script>

<style>

</style>
