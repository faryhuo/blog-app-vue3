<template>
    <nav class="navbar navbar-dark bg-primary">
       <a href="" class="navbar-brand">List</a>
       <ul v-if="!user.isLogin" class="list-inline mb-0">
         <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">Sign in</a></li>
         <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">Sign Up</a></li>
       </ul>
        <ul v-else class="list-inline mb-0">
         <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">Hello {{user.name}}</a></li>
       </ul>
    </nav>
</template>

<script lang="ts">

import { defineComponent, PropType } from 'vue'

export interface UserProps{
  isLogin: boolean;
  id?:number;
  name?:string;
}

export default defineComponent({
  name: 'GlobalHeader',
  props: {
    user: {
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
