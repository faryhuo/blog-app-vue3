<template>
  <div class="container">
    <global-header :user="user"/>
    <column-list :list="list"/>
    <ValidationForm @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">Email</label>
        <validation-input ref="inputRef" :rules="emailRules" v-model="emailValue" placeholder="fff"/>
      </div>
      <div>{{emailValue}}</div>
      <!-- <template #submit>
        <span>submit</span>
      </template> -->
    </ValidationForm>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList from '@/components/ColumnList/ColumnList.vue'
import ValidationInput, { RulesProps } from '@/components/ValidationInput/ValidationInput.vue'
import GlobalHeader, { UserProps } from '@/components/GlobalHeader/GlobalHeader.vue'
import testData from '@/testData/columnList'
import ValidationForm from '@/components/ValidationForm/ValidationForm.vue'

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
    ValidationInput,
    ValidationForm
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
    const inputRef = ref<any>()
    const onFormSubmit = (result: boolean) => {
      console.log(inputRef.value.validateInput())
    }

    return {
      list: testData,
      user: currentUser,
      emailRef,
      emailRules,
      emailValue,
      onFormSubmit,
      inputRef
    }
  }
})
</script>

<style>

</style>
