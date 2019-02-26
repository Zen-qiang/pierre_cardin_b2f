<template>
  <div class="partner">
    <div class="empty"></div>
    <div class="container">
      <h4>合伙人主页</h4>
      <p class="detail">xxxx公司</p>
      <div class="content">
        <div class="box">
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-15_18-57-52.jpg" alt="">
            <p>样品上传</p>
          </div>
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-20_23-09-15.jpg" alt="">
            <p>订单管理</p>
          </div>
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-20_23-09-32.jpg" alt="">
            <p>合同管理</p>
          </div>
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-20_23-09-43.jpg" alt="">
            <p>发票管理</p>
          </div>
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-20_23-09-50.jpg" alt="">
            <p>结算单</p>
          </div>
          <div class="item">
            <img src="../../../static/Snipaste_2019-02-20_23-10-10.jpg" alt="">
            <p>报表分析</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import b2fAjax from '../../server/b2fAjax.js'
export default {
  created () {
    this.getUrl()
  },
  methods: {
    getUrl () {
      const token = sessionStorage.getItem('token')
      b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.get.getRedirectUrl","token":"${token}"}}]`})
    }
  }
}
</script>

<style lang="scss" scoped>
.partner {
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
  padding: 0.4rem 0 0.08rem;
}
h4, h5, h6, p {
  margin: 0;
}
p {
  font-size: 0.01rem;
}
.container {
  text-align: center;
}
.detail {
  font-size: 0.1rem;
  color: #999;
  letter-spacing: 0.04rem;
}
.content {
  margin: 0.3rem auto 0;
  max-width: 6.4rem;
  overflow: hidden;
}
.box {
  display: flex;
  flex-flow: row wrap;
  justify-content: space-between;
  font-size: 0;
}
.item {
  border-radius: 0.02rem;
  box-shadow: 0 0 0.1rem #f7f7f7;
  box-sizing: border-box;
  display: inline-block;
  background: #fff;
  flex: 0 0 30%;
  margin-bottom: 0.2rem;
  padding: 0.2rem;
  cursor: pointer;
  &:hover {
    box-shadow: 0 0 0.2rem #f2f2f2;
  }
  p {
    font-size: 0.15rem;
    margin-top: 0.1rem;
  }
}
</style>

