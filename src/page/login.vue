<template>
  <div class="partnerLogin">
    <div class="empty"></div>
    <div class="container">
      <h4>商品供应合伙人登陆</h4>
      <p class="detail">请输入您的手机号码</p>
      <form class="formContent" @submit.prevent>
        <div>
          <p><span>手机号码 *</span></p>
          <p><input type="tel" placeholder="输入您的手机号码" v-model="username" required></p>
        </div>
        <div>
          <p><span>密码 *</span></p>
          <p><input type="password" placeholder="输入您的密码" v-model="password" @keydown.enter.prevent="login" required></p>
        </div>
        <p class="message"><span>{{message}}</span></p>
        <p><button class="login" @click="login">登陆</button></p>
        <p><button class="join" @click="$router.push({name: 'partnerJoin'})">申请加入</button></p>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      username: '',
      password: '',
      message: ''
    }
  },
  methods: {
    login () {
      // this.message = ''
      // if (!this.username && !this.password) return
      // b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"username":"${this.username}","password":"${this.password}","cmd":"b2b.login"}}]`}).then(res => {
      //   sessionStorage.setItem('token', res.result.token)
      //   this.checkPayStatu(res.result.token)
      // }).catch(err => {
      //   this.message = err.message
      // })
    },
    checkPayStatu (token) {
      // b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.valid.paystatus","token":"${token}"}}]`}).then(res => {
      //   // console.log(res)
      //   if (res.result.payStatus === 'Y') {
      //     this.$router.push({name: 'partner'})
      //   } else {
      //     this.$router.push({name: 'payPage'})
      //   }
      // }).catch(err => {
      //   console.log(err)
      // })
    }
  }
}
</script>

<style lang="scss" scoped>
.partnerLogin {
  min-height: 100vh;
  font-family: PingFangSC-Semibold,PingFangSC-Regular,"微软雅黑",Microsoft YaHei !important;
  background: #f8f8ee;
}
.empty {
  height: 88px;
  background: #fff;
}
h4 {
  font-size: 0.2rem;
  padding: 0.4rem 0 0.1rem;
}
p {
  font-size: 0.1rem;
}
h4, h5, h6, p {
  margin: 0;
}
input {
  background: none;
  border: 1px solid #999;
  height: 0.3rem;
  padding: 0 0.1rem;
  width: 3rem;
  // outline: none;
}
button {
  width: 100%;
  border: none;
  color: #fff;
  height: 0.3rem;
}
.container {
  text-align: center;
}
.formContent {
  display: inline-block;
  text-align: initial;
  padding-top: 0.4rem;
}
.detail {
  color: #999;
  letter-spacing: 0.04rem;
}
.login {
  background: #5b686d;
}
.join {
  background: #c42c02;
}
.formContent > div > p:first-of-type {
  margin-bottom: 0.08rem;
}
.formContent > div > p:last-of-type {
  margin-bottom: 0.1rem;
}
.formContent > p {
  margin-bottom: 0.1rem;
}
.message {
  height: 0.12rem;
  text-align: center;
  font-size: 0.08rem;
  color: #c42c02;
}
</style>
