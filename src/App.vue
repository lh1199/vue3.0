<template>
  <div class="container">
    <global-header :user="crrentUser"></global-header>
    <validate-form action="" @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input :rules="emailRules" v-model="emailVal" type="text" placeholder="请输入邮箱地址" ref="inputRef"></validate-input>
      </div>
      <div class="mb-3">
        <label class="form-label">密码</label>
        <validate-input :rules="passwordRules" v-model="passwordVal" type="password" placeholder="请输入密码"></validate-input>
      </div>
    </validate-form>
    <column-list :list="list"></column-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import ValidateForm from './components/ValidateForm.vue'
const crrentUser: UserProps = {
  isLogin: true,
  name: 'lh1199',
  id: 1
}
const testData: ColumnProps[] = [{
  id: 1,
  title: 'test1的专栏',
  description: '这是test1的专栏',
  avatar: './assets/logo.png'
}, {
  id: 2,
  title: 'test2的专栏',
  description: '这是test2的专栏',
  avatar: './assets/logo.png'
}, {
  id: 3,
  title: 'test3的专栏',
  description: '这是test3的专栏',
  avatar: './assets/logo.png'
}, {
  id: 4,
  title: 'test4的专栏',
  description: '这是test4的专栏'
}]

export default defineComponent({
  name: 'App',
  components: {
    ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup () {
    const inputRef = ref<any>()
    const emailVal = ref('123@test.com')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]
    const passwordVal = ref('123')
    const passwordRules: RulesProp = [
      { type: 'required', message: '密码不能为空' }
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const onFormSubmit = (result: boolean) => {
      console.log('result', result)
    }
    return {
      list: testData,
      crrentUser,
      emailRef,
      emailRules,
      emailVal,
      passwordVal,
      passwordRules,
      onFormSubmit,
      inputRef
    }
  }
})
</script>

<style>

</style>
