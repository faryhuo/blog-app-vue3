<template>
  <div class="dropdown btn-group">
    <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">{{title}}</a></li>
    <ul class="dropdown-menu">
        <slot/>
    </ul>
  </div>
</template>

<script lang="ts">

import { defineComponent } from 'vue'

export default defineComponent({
  name: 'DropDownList',
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
