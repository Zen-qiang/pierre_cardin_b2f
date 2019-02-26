<template>
  <div class="partnerSuccess">
    <div class="empty"></div>
    <div class="container">
      <p class="icon"><img src="../../../static/success.svg" alt=""></p>
      <h4>申请成功</h4>
      <p class="mes">“xxx，你好！您的申请我们已经收到。”</p>
      <p class="detail">我们的业务人员将会尽快联系您！请您耐信等待！</p>
      <p class="action"><button>返回官网</button></p>
    </div>
  </div>
</template>
<style lang="scss" scoped>
.partnerSuccess {
  min-height: 100vh;
  font-family: PingFangSC-Semibold,PingFangSC-Regular,"微软雅黑",Microsoft YaHei !important;
  background: #f8f8ee;
}
.empty {
  height: 88px;
  background: #fff;
}
h4, p {
  margin: 0;
}
h4 {
  font-size: 0.2rem;
  margin-bottom: 0.3rem;
}
p {
  font-size: 0.1rem;
}
.container {
  text-align: center;
  font-size: 0.1rem;
}
.icon {
  margin: 0.7rem 0 0.3rem;
  display: inline-block;
  width: 0.5rem;
  height: 0.5rem;
  border: 0.02rem solid #c42c02;
  border-radius: 50%;
  img {
    width: 100%;
    padding: 10%;
  }
}
.mes {
  font-size: 0.14rem;
  color: #999;
  line-height: 0.3rem;
}
.detail {
  font-size: 0.09rem;
  color: #999;
}
.action {
  margin-top: 0.4rem;
  button {
    background: #c42c02;
    color: #fff;
    font-size: 0.1rem;
    border: none;
    line-height: 0.3rem;
    width: 1.5rem;
    cursor: pointer;
  }
}
</style>
