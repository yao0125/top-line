<template>
<div>
 <van-nav-bar title="登录" />
    <van-cell-group>
      <van-field
        v-model="user.mobile"
        required
        clearable
        label="手机"
        v-validate='required'
        placeholder="请输入手机号"
      />
      <van-field
        v-model="user.code"
        type="password"
        label="验证码"
        placeholder="请输入验证码"
        required
      />
    </van-cell-group>
    <div class="login-btn">
        <van-button type="info"  @click="onLogin">登录</van-button>
    </div>
</div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'Login',
  data () {
    return {
      user: {
        mobile: '',
        code: '',
        isLoginLoading: false
      }

    }
  },
  methods: {
    async onLogin () {
      try {
        const { data } = await axios({
          method: 'POST',
          url: 'http://ttapi.research.itcast.cn/app/v1_0/authorizations',
          data: this.user
          // 跳转到首页
          // this.$router.push({name：'Home'})
        })
        console.log(data)
      } catch (err) {
        if (err.response && err.resopnse.status === 400) { this.$totast.fail('手机号或验证码错误') }
      }
    },
    isLoginLoading () {

    }

  }
}
</script>
<style scoped lang='less'>
.login-btn {
    padding:20px;
    .van-button{
        width:100%;
    }
}
</style>
