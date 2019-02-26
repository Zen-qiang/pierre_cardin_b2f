<template>
  <div class="pay">
    <div class="empty"></div>
    <div class="container">
      <h4>保证金条款</h4>
      <p class="detail">请详细阅读条款内容</p>
      <div class="content">
        <div class="provision">
          <p>内容保保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容保证金条款内容</p>
        </div>
        <div class="agree">
          <p class="form">
            <label><input type="checkbox" v-model="isCheck"><span></span></label>
          </p>
          <p class="text">我已详细了解并同意上述保证金条款</p>
        </div>
        <div class="action"><button :class="{active: isCheck}" :disabled="!isCheck && !payWay" @click="toPay">支付保证金</button></div>
      </div>
    </div>
    <div class="modal fade" id="payModal" role="dialog" aria-hidden="false" data-backdrop="static">
      <div class="modal-dialog modal-lg" role="document">
        <div class="modal-content">
          <div class="payModelContent">
            <div class="payInfo" v-if="payStatu === 1">
              <h4>在线支付</h4>
              <div class="payInfo_info">
                <p><span>收款方</span><span>海瀚云商（上海）实业股份有限公司</span></p>
                <p><span>支付内容</span><span>保证金</span></p>
                <!-- <p><span>订单编号</span><span>皮卡</span></p> -->
              </div>
              <hr>
              <div class="payInfo_way">
                <h6>支付方式</h6>
                <ul>
                  <li><label ><input type="radio" value="yinlian" v-model="payWay"><p><img src="../../../static/yinlian.jpg" alt=""></p></label></li>
                  <li class="middle"><label ><input type="radio" value="zhifubao" v-model="payWay"><p><img src="../../../static/zhifubao.jpg" alt=""></p></label></li>
                  <li><label ><input type="radio" value="weixin" v-model="payWay"><p><img src="../../../static/weixin.jpg" alt=""></p></label></li>
                </ul>
              </div>
              <hr>
              <div class="payInfo_action">
                <p><span>支付金额</span><span>￥{{bailAmt}}</span></p>
              </div>
              <p><button :class="{active: payWay}" @click="pay" :disabled="!payWay">立即支付</button></p>
            </div>
            <div class="payIng" v-if="payStatu === 2">
              <h4>支付宝付款</h4>
              <p class="detail">打开支付宝扫一扫付款</p>
              <p class="payIng_info"><span>支付金额 </span><span>￥{{bailAmt}}</span></p>
              <div class="payIng_code"><div ref="qrcodeContainer"><div id="qrcode" ref="qrcode"></div></div></div>
            </div>
            <div class="paySuccess" v-if="payStatu === 3">
              <h4>支付成功</h4>
              <p class="detail">您已成为B2F正式用户</p>
              <p class="paySuccess_icon"><img src="../../../static/success.svg" alt=""></p>
              <p class="paySuccess_action"><button @click="loginNow">立即登陆</button></p>
            </div>
            <button v-show="payStatu !== 3" type="button" class="close pay-dialog-close" data-dismiss="modal" aria-label="Close" @click.stop="close">
              <span aria-hidden="true"><img src="../../../static/xxx.svg"/></span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import b2fAjax from '../../server/b2fAjax.js'
import QRCode from 'qrcodejs2'
export default {
  data () {
    return {
      isCheck: false,
      payStatu: 1,
      payWay: '',
      timmer: null,
      bailAmt: ''
    }
  },
  methods: {
    toPay () {
      if (!this.isCheck && !this.payWay) return
      $("#payModal").modal("show")
      this.getMoney()
      // $("#payModal").appendTo("body");
    },
    close () {
      if (this.timmer !== null) clearInterval(this.timmer)
      $("#payModal").modal("hide")
      setTimeout(() => {
        this.payStatu = 1
        this.payWay = ''
      }, 300)
    },
    pay () {
      if (!this.payWay) return
      this.payStatu = 2
      this.getPayInfo()
    },
    loginNow () {
      $("#payModal").modal("hide")
      this.$router.push({name: 'partner'})
    },
    getPayInfo () {
      b2fAjax({"transactions":'[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.paycode.get","payType":"normal"}}]'}).then(res => {
        const width = this.$refs.qrcodeContainer.clientWidth
        let qrcode = new QRCode(this.$refs.qrcode, {
          text: res.result.billQRCode,
          width: width,
          height: width
        })
        if (this.timmer !== null) clearTimeout(this.timmer)
        this.timmer = setInterval(() => {
          this.checkPayStatu(res.result.billNo)
        }, 3000)
      })
    },
    checkPayStatu (billNo) {
      b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.payment.status.get","billNo":${billNo}}}]`}).then(res => {
        if (res.code === 0) {
          if (res.result.status === 'SUCCESS') {
            clearInterval(this.timmer)
            this.payStatu = 3
          }
        }
      }).catch(err => {
        console.log(err)
      })
    },
    getMoney () {
      const token = sessionStorage.getItem('token')
      b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.get.paybailamt","token":"${token}"}}]`}).then(res => {
        console.log(res.result.bailAmt)
        this.bailAmt = res.result.bailAmt
      })
      // b2fAjax({"transactions":`[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.get.supplierDataList","token":"${token}"}}]`})
    }
  }
}
</script>

<style lang="scss" scoped>
.pay {
  min-height: 100vh;
  font-family: PingFangSC-Semibold,PingFangSC-Regular,"微软雅黑",Microsoft YaHei !important;
  background: #f8f8ee;
}
.empty {
  height: 88px;
  background: #fff;
}
.container {
  text-align: center;
}
h4, p {
  margin: 0;
}
h4 {
  font-size: 0.2rem;
  margin-top: 0.4rem;
}
p {
  font-size: 0.1rem;
}
.detail {
  color: #999;
  letter-spacing: 0.01rem;
}
.provision {
  margin: 0.3rem 0;
  p {
    width: 3rem;
    background: #fff;
    border: 1px solid #999;
    margin: 0 auto;
    padding: 0.1rem;
    font-size: 0.08rem;
    line-height: 0.16rem;
    max-height: 3rem;
    overflow: auto;
  }
}
.agree {
  font-size: 0;
  p {
    display: inline-block;
    vertical-align: middle;
  }
  span {
    display: inline-block;
    width: 0.08rem;
    height: 0.08rem;
  }
  input {
    display: none;
  }
  .form {
    width: 0.14rem;
    height: 0.14rem;
    border: 1px solid #999;
    text-align: center;
    line-height: 0.14rem;
    margin-right: 0.06rem;
  }
  :checked + span {
    background: #c42c02;
  }
}
.action {
  font-size: 0;
  margin: 0.2rem 0;
}
.action button {
  width: 1.4rem;
  font-size: 0.1rem;
  height: 0.3rem;
  background: #999;
  color: #fff;
  border: none;
  &.active {
    background: #c42c02;
  }
}
.modal-content {
  width: 4rem;
  background: none;
  margin: 0 auto;
}
.payModelContent {
  position: relative;
  // width: 3rem;
  // margin: 0 auto;
  h4 {
    margin: 0;
    text-align: center;
  }
  hr {
    margin: 0;
  }
  .detail {
    text-align: center;
  }
  .payInfo, .payIng, .paySuccess {
    background: #fff;
    padding: 0.3rem;
    margin: 0 auto;
  }
  .closePay {
    position: absolute;
    top: 0.1rem;
    right: 0.1rem;
    width: 0.2rem;
    height: 0.2rem;
    background: #c42c02;
  }
  .pay-dialog-close {
    position: absolute;
    top: 0.1rem;
    right: 0.1rem;
  }
  .payInfo {
    > div {
      padding: 0.2rem 0;
    }
    .payInfo_info {
      p {
        display: flex;
        flex-flow: row nowrap;
        justify-content: space-between;
        align-items: center;
        height: 0.3rem;
        > span:last-of-type {
          color: #d35d3a;
        }
      }
    }
    .payInfo_way {
      h6 {
        font-size: 0.1rem;
        margin: 0;
        color: #999;
      }
      ul {
        display: flex;
        flex-flow: row nowrap;
        margin: 0.1rem 0 0;
        padding: 0;
        list-style: none;
        li {
          flex: 1;
          font-size: 0;
          &.middle {
            border-left: 1px solid rgba(0, 0, 0, .1);
            border-right: 1px solid rgba(0, 0, 0, .1);
          }
          label {
            margin: 0!important;
          }
          input {
            display: none;
          }
          p {
            text-align: center;
            padding: 0 0.1rem;
          }
          img {
            width: 100%;
            vertical-align: middle;
            border: 2px solid #fff;
          }
          :checked + p img {
            border-color: #318efc;
          }
        }
      }
    }
    .payInfo_action {
      p {
        display: flex;
        flex-flow: row nowrap;
        justify-content: space-between;
        align-items: center;
        span {
          color: #999;
        }
        > span:last-of-type {
          color: #c42c02;
          font-size: 0.2rem;
        }
      }
    }
    > p {
      text-align: center;
      button {
        width: 1.4rem;
        background: #999;
        border: none;
        color: #fff;
        height: 0.3rem;
        &.active {
          background: #c42c02;
        }
      }
    }
  }
  .payIng {
    text-align: center;
    h4 {
      margin-bottom: 0.1rem;
    }
    .payIng_info {
      margin: 0.3rem 0;
    }
    .payIng_code {
      width: 1.2rem;
      height: 1.2rem;
      margin: auto;
      border: 1px solid rgba($color: #000000, $alpha: .1);
      padding: 0.06rem;
    }
  }
  .paySuccess {
    text-align: center;
    h4 {
      margin-bottom: 0.1rem;
    }
    .paySuccess_icon {
      margin: 0.4rem auto;
      width: 0.5rem;
      height: 0.5rem;
      border: 0.02rem solid #c42c02;
      border-radius: 50%;
      img {
        width: 100%;
        padding: 10%;
      }
    }
    .paySuccess_action {
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
  }
}
</style>
