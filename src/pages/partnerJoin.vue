<template>
  <div class="partnerJoin">
    <div class="empty"></div>
    <div class="container">
      <h4>申请加入合伙人</h4>
      <p class="detail">填写相关信息以便我们联络您</p>
      <div class="formContainer">
        <form enctype="multipart/form-data" @submit.prevent="checkForm">
          <section>
            <h6>基本信息</h6>
            <div class="content">
              <div>
                <label>
                  <p class="labelText"><span>名称</span></p>
                  <p><input type="text" placeholder="请输入您的工厂名称" v-model.lazy="supplierName" required></p>
                </label>
              </div>
              <div>
                <label>
                  <p class="labelText"><span>地址</span></p>
                  <p><input type="text" placeholder="请输入您的工厂地址" v-model="supplierAddress" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>联系人</span></p>
                  <p><input type="text" placeholder="请输入联系人" v-model="contacts" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>Email</span></p>
                  <p><input type="email" placeholder="请输入您的邮箱" v-model="email" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>手机号</span></p>
                  <p><input type="tel" placeholder="请输入您的手机号" v-model="phone" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>密码</span></p>
                  <p><input type="password" placeholder="请输入您的密码" v-model="password" required></p>
                </label>
              </div>
              <!-- <div>
                <label>
                  <p class="labelText"><span>您的地区</span></p>
                  <p><input type="text" placeholder="省/市/区"></p>
                </label>
              </div> -->
            </div>
            <hr>
          </section>
          <section>
            <h6>经营状况</h6>
            <div class="content">
              <div class="half">
                <label>
                  <p class="labelText"><span>生产值</span></p>
                  <p><input type="text" placeholder="请输入您的生产值" v-model="outputYear" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>内外销占比</span></p>
                  <p><input type="text" placeholder="请输入您的占比" v-model="saleRatio" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>管理层/基层人数</span></p>
                  <p><input type="text" placeholder="请输入联系人" v-model="peopleNum" required></p>
                </label>
              </div>
              <div>
                <label>
                  <p class="labelText"><span>合作品牌</span></p>
                  <p><textarea placeholder="请输入您的合作品牌以: 分隔" rows="4" v-model="brand" required></textarea></p>
                </label>
              </div>
            </div>
            <hr>
          </section>
          <section>
            <h6>经营品类</h6>
            <div class="content checkContent" v-for="(value, key, index) in supplierType" :key="index">
              <div class="check" v-for="(val, idx) in value" :key="idx">
                <label>
                  <p class="checkCustom"><input type="checkbox" :value="val" v-model="supplierTypes"><span></span></p>
                  <p><span>{{val}}</span></p>
                </label>
              </div>
            </div>
            <hr>
          </section>
          <section>
            <h6>开票信息</h6>
            <div class="content">
              <div>
                <label>
                  <p class="labelText"><span>名称</span></p>
                  <p><input type="text" placeholder="请输入您的名称" v-model="invoiceName" required></p>
                </label>
              </div>
              <div>
                <label>
                  <p class="labelText"><span>纳税人识别号</span></p>
                  <p><input type="text" placeholder="请输入您的识别号" v-model="invoiceCode" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>地址</span></p>
                  <p><input type="text" placeholder="请输入地址" v-model="invoiceAddress" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>电话</span></p>
                  <p><input type="text" placeholder="请输入电话" v-model="invoicePhone" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>开户行</span></p>
                  <p><input type="text" placeholder="请输入开户行" v-model="invoiceBank" required></p>
                </label>
              </div>
              <div class="half">
                <label>
                  <p class="labelText"><span>开户账号</span></p>
                  <p><input type="text" placeholder="请输入开户账号" v-model="invoiceNum" required></p>
                </label>
              </div>
            </div>
            <hr>
          </section>
          <section>
            <h6>附件上传</h6>
            <div class="content fileContent">
              <div class="triplet">
                <label>
                  <p class="labelText"><span>营业执照</span></p>
                  <p class="hide"><input type="file" accept="image/png, image/jpeg, image/gif, image/jpg" @change="tirggerFile($event)"></p>
                  <p class="fileBox">
                    <span v-if="!yyzzImg"></span>
                    <img v-else :src="yyzzImg">
                  </p>
                </label>
              </div>
              <div class="triplet">
                <label>
                  <p class="labelText"><span>开户证明</span></p>
                  <p class="hide"><input type="file" accept="image/png, image/jpeg, image/gif, image/jpg" @change="tirggerFile($event)"></p>
                  <p class="fileBox">
                    <span v-if="!khzmImg"></span>
                    <img v-else :src="khzmImg">
                  </p>
                </label>
              </div>
            </div>
          </section>
          <div class="submit"><input type="submit" value="立即提交"></div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import b2fAjax from '../../server/b2fAjax.js'
import formate from '../../server/formate.js';
export default {
  data () {
    return {
      supplierName: '', // 工厂名称
      supplierAddress: '', // 工厂地址
      contacts: '', // 联系人
      phone: '', // 联系电话
      password: '', // 登陆密码
      email: '', // 收件邮箱
      outputYear: '', // 年产值
      saleRatio: '', // 内外销占比
      peopleNum: '', // 管理层/基层人数
      brand: '', // 合作品牌
      invoiceName: '', // 开票信息名称
      invoiceCode: '', // 纳税人识别号
      invoiceAddress: '', // 开票地址
      invoicePhone: '', // 开票电话
      invoiceBank: '', // 开户银行
      invoiceNum: '', // 开户账号
      yyzzfile: null, // 营业执照
      khzmfile: null, // 开户证明
      supplierTypes: [], // 供应商经营品类
      supplierType: {}, // 经营品类
      yyzzImg: '',
      khzmImg: ''
    }
  },
  computed: {
    
  },
  created () {
    this.getSupplierType()
  },
  watch: {
    supplierName (newVal, oldVal) {
      if (oldVal !== newVal) {
        b2fAjax({"transactions":'[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.valid.suppliername","supplierName":"'+newVal+'"}}]'})
      }
    }
  },
  methods: {
    getSupplierType () {
      b2fAjax({"transactions":'[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.supplier.type.get"}}]'}).then(res => {
        this.supplierType = res.result
      }).catch(err => {
        console.log(err)
      })
    },
    tirggerFile (event) {
      console.dir(event.target)
      const that = this
      let file = event.target.files[0]
      if (!file.size) return
      let reader = new FileReader()
      reader.readAsDataURL(file)
      reader.onload = function () {
        that.khzmImg = this.result
      }

      var formData = new FormData(this);
      formData.append("Filedata",file)//传给后台的file的key值是可以自己定义的
      formData.append("query",JSON.stringify('typeData'))
      formData.append('command', 'com.agilecontrol.phone.B2BCmd')
      formData.append('cmd', 'b2f.insert.supplier.get')
      formData.append('nds.control.ejb.UserTransaction', 'N')
      formData.append("factoryName", "南京")
      formData.append('sequence', '1')
      // b2fAjax(formData, 'http://www.pc18.vip/c/fileupload3')
      $.ajax({
        url: 'http://www.pc18.vip/c/fileupload3',
        cache: false,
        // xhrFields: { withCredentials: true },
        processData:false, // 对data参数进行序列化处理，默认值是true。默认情况下发送的数据将被转换为对象
        async: true, 
        contentType: false,
        // contentType: 'multipart/form-data',
        // contentType: 'application/x-www-form-urlencoded',
        data: formData,
        type: "post",
        success: function (res) {
          console.log(res)
          if (res.length) {
            const result = res[0]
            if (result.code === 0) {
              console.log(result)
            }
          }
        },
        error: function(err) {
          console.log(err)
        }
      })
    },
    checkForm (e) {
      b2fAjax({"transactions":'[{"id":1,"command":"com.agilecontrol.phone.B2BCmd","params":{"cmd":"b2f.valid.suppliername","supplierName":"'+that.supplierName+'"}}]'})
      e.preventDefault()
    }
  }
}
</script>
<style lang="scss" scoped>
.partnerJoin {
  min-height: 100vh;
  font-family: PingFangSC-Semibold,PingFangSC-Regular,"微软雅黑",Microsoft YaHei !important;
  background: #f8f8ee;
  padding-bottom: 1rem;
}
.empty {
  height: 88px;
  background: #fff;
}
h4, h6, p, label {
  margin: 0;
}
h4 {
  font-size: 0.2rem;
  margin: 0.4rem 0 0;
}
p {
  font-size: 0.1rem;
}
.detail {
  color: #999;
}
h4 + p.detail {
  margin-bottom: 0.3rem;
  letter-spacing: 0.01rem;
}
h6 {
  font-size: 0.16rem;
}
input::-webkit-input-placeholder, textarea::-webkit-input-placeholder { /*WebKit browsers*/
  color: #999;
}

input::-moz-input-placeholder, textarea::-moz-input-placeholder { /*Mozilla Firefox*/
  color: #999;
}

input::-ms-input-placeholder, textarea::-ms-input-placeholder { /*Internet Explorer*/ 
  color: #999;
}
.container {
  > h4, > p {
    text-align: center;
  }
}
.formContainer {
  section {
    h6 {
      margin-bottom: 0.1rem;
    }
    label {
      width: 100%;
    }
    p {
      line-height: 0.24rem;
    }
    input, textarea {
      width: 100%;
      border: 1px solid #999;
      background: none;
      padding: 0 0.1rem;
    }
    textarea {
      resize: none;
    }
    hr {
      margin: 0.4rem 0;
      border-top: 1px solid #999;
    }
  }
  .content {
    display: flex;
    flex-flow: row wrap;
    justify-content: space-between;
    &.checkContent {
      justify-content: flex-start;
      margin-right: -0.2rem;
    }
    > div {
      font-size: 0;
      flex: 0 0 100%;
      &.half {
        flex: 0 0 48%;
      }
      &.check {
        flex: 0 0 auto;
        margin-right: 0.2rem;
        p {
          display: inline-block;
          vertical-align: middle;
          line-height: 0.3rem;
          span {
            display: inline-block;
            vertical-align: middle;
            line-height: 0.2rem;
            user-select: none;
          }
        }
        .checkCustom {
          margin-right: 0.08rem;
          input {
            display: none;
          }
          span {
            width: 0.14rem;
            height: 0.14rem;
            border: 1px solid #999;
            position: relative;
          }
          :checked + span::after {
            content: '';
            display: inline-block;
            position: absolute;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            width: 0.08rem;
            height: 0.08rem;
            background: #c42c02;
            margin: auto;
          }
        }
      }
    }
    .labelText {
      span {
        display: inline-block;
        &::after {
          content: '*';
          display: inline-block;
          text-align: start;
          margin-left: 0.02rem;
        }
      }
    }
    &.fileContent {
      justify-content: flex-start;
      .triplet {
        flex: 0 0 30%;
        margin-right: 3%;
      }
      .hide {
        display: none; 
      }
      .fileBox {
        cursor: crosshair;
        padding-bottom: 60%;
        position: relative;
        span, img {
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
        }
        span {
          color: #999;
          display: block;
          border: 1px dashed #999;
          background: transparent no-repeat center;
          background-image: linear-gradient(to top, currentColor, currentColor), linear-gradient(to top, currentColor, currentColor);
          background-size: 20% 1px, 1px 30%;
        }
        img {
          border: 1px solid #999;
          object-fit: contain;
        }
      }
    }
  }
}
.submit {
  text-align: center;
  input {
    width: 1.4rem;
    font-size: 0.1rem;
    height: 0.3rem;
    background: #c42c02;
    border: none;
    color: #fff;
  }
}
</style>
