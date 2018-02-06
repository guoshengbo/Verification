<template>
<div>
  <el-input :type="textarea" v-model="input" :placeholder="placeholder" @change='checkinput' :class="checkclass"></el-input>
  <div v-if="!showinput" class="el-form-item__error">
    请输入正确格式的{{typename}}
  </div>
</div>
</template>
<script>
  export default {
    data () {
      return {
        showinput: true,
        input: '',
        checkclass: '',
        regList: {
          ImgCode: /^[0-9a-zA-Z]{4}$/,
          SmsCode: /^\d{4}$/,
          MailCode: /^\d{4}$/,
          UserName: /^[\w|\d]{4,16}$/,
          Password: /^[\w!@#$%^&*.]{6,16}$/,
          Mobile: /^1[3|4|5|7|8]\d{9}$/,
          RealName: /^[\u4e00-\u9fa5|·]{2,16}$|^[a-zA-Z|\s]{2,20}$/,
          BankNum: /^\d{10,19}$/,
          Money: /^([1-9]\d*|[0-9]\d*\.\d{1,2}|0)$/,
          Answer: /^\S+$/,
          IDcard: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/
        }
      }
    },
    computed: {
      textarea: function () {
        if (this.inputtext === 'textarea') {
          return 'textarea'
        } else {
          return 'text'
        }
      }
    },
    props: ['placeholder', 'type', 'typename', 'changeshow', 'inputtext'],
    methods: {
      checkinput: function () {
        if (!this.regList[this.type].test(this.input)) {
          this.showinput = false
          this.checkclass = 'checkinput'
          this.changeshow(false)
        } else {
          this.showinput = true
          this.checkclass = ''
          this.changeshow(true)
        }
      }
    }
  }
</script>
<style>
.el-form-item__error {
    color: #f56c6c;
    font-size: 12px;
    line-height: 1;
    padding-top: 4px;
    position: absolute;
    top: auto;
    left: auto;
}
.checkinput .el-input__inner{
 border-color: #f56c6c !important;
}
.checkinput .el-textarea__inner{
 border-color: #f56c6c !important;
}
</style>
