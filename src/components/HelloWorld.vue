<template>
  <div class="row">

  </div>
</template>

<script lang="ts">

import { computed, defineComponent, PropType } from 'vue'

export interface UserProps{
    id:number;
    title:string;
    avatar?:string;
    description: string;
}

export default defineComponent({
  name: 'GlobalHeader',
  props: {
    list: {
      type: Object as PropType<UserProps>,
      required: true
    }
  },
  setup (props) {
    return {
    }
  }
})

</script>

<style>

</style>
