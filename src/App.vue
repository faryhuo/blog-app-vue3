<template>
  <div class="container">
    <global-header :user="user"/>
    <column-list :list="list"/>
    <form>
      <div class="mb-3">
        <label class="form-label">Email</label>
        <validation-input :rules="emailRules" v-model="emailValue" placeholder="fff"/>
      </div>
      <div>{{emailValue}}</div>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList from '@/components/ColumnList/ColumnList.vue'
import ValidationInput, { RulesProps } from '@/components/ValidationInput/ValidationInput.vue'
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
    ColumnList,
    GlobalHeader,
    ValidationInput
  },
  setup () {
    const emailRules: RulesProps = [{
      type: 'required',
      message: 'cannot be empty'
    }, {
      type: 'email',
      message: 'email format is incorrect'
    }]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const emailValue = ref('')

    return {
      list: testData,
      user: currentUser,
      emailRef,
      emailRules,
      emailValue
    }
  }
})
</script>

<style>

</style>
