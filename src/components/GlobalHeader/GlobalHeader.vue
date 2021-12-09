<template>
    <nav class="navbar navbar-dark bg-primary">
       <a href="" class="navbar-brand">List</a>
       <ul v-if="!user.isLogin" class="list-inline mb-0">
         <li class="list-inline-item"><a href="#" class="btn btn-outline-light">Sign in</a></li>
         <li class="list-inline-item"><a href="#" class="btn btn-outline-light">Sign Up</a></li>
       </ul>
        <ul v-else class="list-inline mb-0">
          <drop-down-list :title="`Hello ${user.name}`">
            <drop-down-list-item> <a href="#" class="dropdown-item">New</a></drop-down-list-item>
            <drop-down-list-item :disabled="true"> <a href="#" class="dropdown-item">1</a></drop-down-list-item>
            <drop-down-list-item> <a href="#" class="dropdown-item">Sign out</a></drop-down-list-item>
          </drop-down-list>
       </ul>
    </nav>
</template>

<script lang="ts">

import { defineComponent, PropType } from 'vue'
import { DropDownList, DropDownListItem } from '@/components'

export interface UserProps{
  isLogin: boolean;
  id?:number;
  name?:string;
}

export default defineComponent({
  name: 'GlobalHeader',
  components: {
    DropDownList,
    DropDownListItem
  },
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
