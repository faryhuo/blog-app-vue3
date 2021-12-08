<template>
    <li><a class="dropdown-item" href="#">{{title}}</a></li>
</template>

<script lang="ts">

import { defineComponent } from 'vue'

export default defineComponent({
  name: 'DropDownListItem',
  props: {
    title: {
      type: String,
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
