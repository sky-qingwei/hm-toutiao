<template>
  <div class="container">
    <van-nav-bar title="登录" left-arrow @click-left="$router.back()"></van-nav-bar>
    <!-- 手机号  验证码  登录按钮 -->
    <van-cell-group>
      <van-field
        @blur="validMobile"
        :error-message="errorMsg.mobile"
        v-model.trim="userForm.mobile"
        label="手机号"
        placeholder="请输入手机号"
      />
      <van-field
        @blur="validCode"
        :error-message="errorMsg.code"
        v-model.trim="userForm.code"
        label="验证码"
        placeholder="请输入验证码"
      >
        <van-button class="p10" slot="button" size="mini" type="primary">发送验证码</van-button>
      </van-field>
    </van-cell-group>
    <div class="btn_box">
      <van-button type="info" @click="login" block round>登 录</van-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      loginForm: {
        mobile: '13911111111',
        code: '246810'
      },
      // 专门提示信息的
      errMsg: {
        mobile: '',
        code: ''
      }
    }
  },
  methods: {
    checkMobile () {
      //  判断 为空 判断格式
      if (!this.loginForm.mobile) {
        this.errMsg.mobile = '手机号不能为空'
        return false
      }
      // 判断格式
      if (!/^1[3-9]\d{9}$/.test(this.loginForm.mobile)) {
        this.errMsg.mobile = '手机格式不正确'
        return false
      }
      this.errMsg.mobile = '' // 清空信息
      return true
    },
    checkCode () {
      if (!this.loginForm.code) {
        this.errMsg.code = '验证码不能为空'
        return false
      }
      if (!/^\d{6}$/.test(this.loginForm.code)) {
        this.errMsg.code = '验证码必须为6位数字'
        return false
      }
      this.errMsg.code = '' // 清空信息
      return true
    },
    // 登录方法
    login () {
      if (this.checkMobile() && this.checkCode()) {
        // 都通过了 表示前端校验通过 还要调用接口
        // 提示消息 表示登录成功
        console.log('校验通过')
      }
    }
  }
}
</script>

<style scoped>
.btn-box {
  padding: 20px;
}
</style>
