<template>
  <div class="container">
    <global-header :user="user"/>
    <router-view></router-view>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { RouterView } from 'vue-router'
import 'bootstrap/dist/css/bootstrap.min.css'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader/GlobalHeader.vue'
import testData from '@/testData/columnList'

const currentUser: UserProps = {
  isLogin: true,
  name: 'fary',
  id: 1
}

export default defineComponent({
  name: 'App',
  components: {
    GlobalHeader,
    RouterView
  },
  setup () {
    return {
      list: testData,
      user: currentUser
    }
  }
})
</script>

<style>

</style>
