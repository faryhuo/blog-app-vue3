<template>
  <div class="container">
    <global-header :user="user"/>
    <column-list :list="list"/>
    <drop-down-list title="User">
      <drop-down-list-item title="Logout"></drop-down-list-item>
    </drop-down-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from '@/components/ColumnList/ColumnList.vue'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader/GlobalHeader.vue'
import DropDownList from './components/DropDownList/DropDownList.vue'
import DropDownListItem from './components/DropDownListItem/DropDownListItem.vue'
export { DropDownList, DropDownListItem } from '@/components'

const testData:ColumnProps[] = [{
  id: 1,
  title: 'test1',
  description: 'test 1 ----- asdsad asd asda asda sdasd sdasd sdas asdas',
  avatar: 'https://static.wixstatic.com/media/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.jpg/v1/fill/w_319,h_239,fp_0.50_0.50,q_90/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.webp'
}, {
  id: 2,
  title: 'test2',
  description: 'test2 ----- asdsad asd asda asda sdasd sdasd sdas asdas',
  avatar: 'https://static.wixstatic.com/media/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.jpg/v1/fill/w_319,h_239,fp_0.50_0.50,q_90/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.webp'
}, {
  id: 1,
  title: 'test3',
  description: 'test 3 ----- asdsad asd asda asda sdasd sdasd sdas asdas',
  avatar: 'https://static.wixstatic.com/media/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.jpg/v1/fill/w_319,h_239,fp_0.50_0.50,q_90/9a03fd_3a3301fccc8e4a8382598a9086633cf8~mv2.webp'
}, {
  id: 1,
  title: 'test4',
  description: 'test 4 ----- asdsad asd asda asda sdasd sdasd sdas asdas'
}]

const currentUser: UserProps = {
  isLogin: false,
  name: 'fary',
  id: 1
}

export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    DropDownList,
    DropDownListItem
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
