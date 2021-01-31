<template>
  <div>
    <!--<van-nav-bar left-arrow @click-left="_routerBack" title="登录" fixed :z-index="10"></van-nav-bar>-->

    <div v-if="loginWay==4" >
      <!--下拉框-->
      <div class="selTel">
        <select v-model="phoneType">
          <option v-for="x in phoneTypes">{{x.name}}</option>
        </select><br>
      </div>
      <!--titel-->
      <div class="regTile">
        <p>
          <span>账号注册</span>
        </p>
      </div>

    </div>

    <div class="nav-con align-center login-con"
         :style="{'background-image':'url(static/img/login/backImg.jpg)'}">
      <!--右上角却换-->
      <div style="height: 30px;">
        <p class="tabbtn">
          <span v-bind:class="{active:loginWay == 1}" @click="loginWay=1" v-show="loginWay===2">账号密码登录</span>
          <span v-bind:class="{active:loginWay == 2}" @click="loginWay=2" v-show="loginWay===1">验证码登录</span>
        </p>
      </div>
      <div class="top-area">
        <van-image src="static/img/login/log.jpg" class="top-logo"></van-image>
        <!--<div>Vant Finance</div>-->
      </div>
      <!--用户名密码登录-->
      <div v-if="loginWay==1">
        <van-cell-group>
          <!--&lt;!&ndash;输入账号&ndash;&gt;-->
          <!--<van-field v-model="userName" left-icon="static/img/login/login_user.png" required clearable label="用户名"-->
                     <!--placeholder="请输入手机号/用户名(随便填)" label-align="left" size="large" maxlength="20"></van-field>-->
          <!--&lt;!&ndash;输入密码&ndash;&gt;-->
          <!--<van-field v-model="password" left-icon="static/img/login/login_pass.png" label="密　码"-->
                     <!--placeholder="请输入密码(随便填)" size="large" required clearable-->
                     <!--:type="showPassword?'text':'password'" maxlength="20"-->
                     <!--:right-icon="'static/img/login/eye_'+(showPassword?'open':'close')+'.png'"-->
                     <!--@click-right-icon="showPassword=!showPassword"></van-field>-->


          <!--输入账号-->
          <van-field v-model="userName" required clearable label="账号"
                     placeholder="手机/邮箱" label-align="left" size="large" maxlength="20"></van-field>
          <!--输入密码-->
          <van-field v-model="password"  label="密　码"
                     placeholder="请输入密码" size="large" required clearable
                     :type="showPassword?'text':'password'" maxlength="20"
                     :right-icon="'static/img/login/eye_'+(showPassword?'open':'close')+'.png'"
                     @click-right-icon="showPassword=!showPassword"></van-field>

        </van-cell-group>
        <div class="forget">
          <p >
            <span  v-bind:class="{active:loginWay == 3}" @click="loginWay=3">忘记密码</span>
          </p>
        </div>
        <!--账密登录按钮-->
        <div class="button-con">
          <van-button type="danger" round class="login-btn" :disabled="!canPwdLogin" @click="onLoginClick">登录
          </van-button>
          <!--<van-button type="danger" plain round class="login-btn" @click="loginWay=3-loginWay">短信登录</van-button>-->
        </div>
        <div>
            <p class="res">
              <span v-bind:class="{active:loginWay == 4}" @click="loginWay=4">免费注册</span>
            </p>
        </div>
      </div>
      <!--验证码登陆-->
      <div v-if="loginWay==2">
        <van-cell-group>
          <!--&lt;!&ndash;输入账号&ndash;&gt;-->
          <!--<van-field v-model="userName" left-icon="static/img/login/login_user.png" required clearable label="手机号"-->
                     <!--placeholder="请输入手机号(随便填)" label-align="left" size="large" maxlength="11"></van-field>-->
          <!--&lt;!&ndash;填写验证码&ndash;&gt;-->
          <!--<van-field v-model="smsCode" clearable label="验证码" placeholder="请输入短信验证码" size="large"-->
                     <!--left-icon="envelop-o" maxlength="6" required>-->
            <!--<van-button slot="button" size="small" plain type="danger" class="send-btn" @click="onSMSSend"-->
                        <!--:disabled="!isSendSMSEnable">-->
              <!--{{getSendBtnText}}-->
            <!--</van-button>-->
          <!--</van-field>-->

          <!--输入账号-->
          <van-field v-model="userName"  required clearable label="账号"
                     placeholder="手机号/邮箱" label-align="left" size="large" maxlength="11"></van-field>
          <!--填写验证码-->
          <van-field v-model="smsCode" clearable label="验证码" placeholder="请输入验证码" size="large"
                   maxlength="6" required>
            <van-button slot="button" size="small" plain type="danger" class="send-btn" @click="onSMSSend"
                        :disabled="!isSendSMSEnable">
              {{getSendBtnText}}
            </van-button>
          </van-field>
        </van-cell-group>
        <div class="forget">
          <p >
            <span>忘记密码</span>
          </p>
        </div>
        <!--账密登录按钮-->
        <div class="button-con">
          <van-button type="danger" round class="login-btn" :disabled="!canSMSLogin" @click="onSMSLogin">登录
          </van-button>
          <!--<van-button type="danger" plain round class="login-btn" @click="loginWay=3-loginWay">账号登录</van-button>-->
        </div>
        <div>
          <p class="res">
            <span v-bind:class="{active:loginWay == 4}" @click="loginWay=4">免费注册</span>
          </p>
        </div>
      </div>
      <!--忘记密码-->
      <div v-if="loginWay==3">
        <van-cell-group>
          <!--输入账号-->
          <van-field v-model="userName"  required clearable label="账号"
                     placeholder="手机号/邮箱" label-align="left" size="large" maxlength="11"></van-field>
          <!--填写验证码-->
          <van-field v-model="smsCode" clearable label="验证码" placeholder="请输入验证码" size="large"
                  maxlength="6" required>
            <van-button slot="button" size="small" plain type="danger" class="send-btn" @click="onSMSSend"
                        :disabled="!isSendSMSEnable">
              {{getSendBtnText}}
            </van-button>
          </van-field>
          <!--输入密码-->
          <van-field v-model="password"  label="输入密码"
                     placeholder="请输入新密码" size="large" required clearable
                     :type="showPassword?'text':'password'" maxlength="20"
                     :right-icon="'static/img/login/eye_'+(showPassword?'open':'close')+'.png'"
                     @click-right-icon="showPassword=!showPassword"></van-field>
        </van-cell-group>
        <!--输入密码-->
        <van-field v-model="password"  label="确认密码"
                   placeholder="请输入确认密码" size="large" required clearable
                   :type="showPassword?'text':'password'" maxlength="20"
                   :right-icon="'static/img/login/eye_'+(showPassword?'open':'close')+'.png'"
                   @click-right-icon="showPassword=!showPassword"></van-field>
        <!--账密登录按钮-->
        <div class="button-con">
          <van-button type="danger" round class="login-btn" :disabled="!canSMSLogin" @click="onSMSLogin">重置
          </van-button>
          <!--<van-button type="danger" plain round class="login-btn" @click="loginWay=3-loginWay">账号登录</van-button>-->
        </div>
      </div>
      <!--账号注册-->
      <div v-if="loginWay==4">
        <van-cell-group>
          <!--输入账号-->
          <van-field v-model="userName" required clearable label="账号"
                     placeholder="手机/邮箱" label-align="left" size="large" maxlength="20"></van-field>
          <!--输入密码-->
          <van-field v-model="password"  label="密码"
                     placeholder="请输入密码" size="large" required clearable
                     :type="showPassword?'text':'password'" maxlength="20"
                     :right-icon="'static/img/login/eye_'+(showPassword?'open':'close')+'.png'"
                     @click-right-icon="showPassword=!showPassword"></van-field>
          <!--填写验证码-->
          <van-field v-model="smsCode" clearable label="验证码" placeholder="请输入验证码" size="large"
                     maxlength="6" required>
            <van-button slot="button" size="small" plain type="danger" class="send-btn" @click="onSMSSend"
                        :disabled="!isSendSMSEnable">
              {{getSendBtnText}}
            </van-button>
          </van-field>

        </van-cell-group>
        <!--按钮-->
        <div class="button-con">
          <van-button type="danger" round class="login-btn" :disabled="!canPwdLogin" @click="onLoginClick">完成注册
          </van-button>
        </div>
        <div>
          <p class="res">
            <span v-bind:class="{active:loginWay == 1}" @click="loginWay=1">账号密码登录</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "login-page",
    data() {
      return {
        userName: '',
        password: '',
        smsCode: '',
        showPassword: false, //是否显示明文
        loginWay: 1, //1: 账密，2：验证码
        smsCountDown: 0,
        smsCountInterval: null,
        phoneTypes:[
          {name:"中国大陆",famname:"中国大陆"},
          {name:"非中国大陆",famname:"非中国大陆"},
        ],
        phoneType:"中国大陆"

      };
    },
    created(){
     this.phoneType =this.phoneTypes[0].name;
    },
    computed: {
      isSendSMSEnable() {
        return this.smsCountDown <= 0 && this.userName.length > 4;
      },
      getSendBtnText() {
        if (this.smsCountDown > 0) {
          return this.smsCountDown + '秒后发送';
        } else {
          return '发送验证码';
        }
      },
      canSMSLogin() {
        return this.userName.length > 4 && this.smsCode.length > 4;LoginPage
      },
      canPwdLogin() {
        return this.userName.length > 4 && this.password.length > 4;
      },
    },
    mounted() {
    },
    beforeDestroy() {
      if (this.smsCountInterval) {
        clearInterval(this.smsCountInterval);
      }
    },
    methods: {
      onSMSSend() {
        this._showLoading();
        setTimeout(() => {
          this._dismissLoading();
          this._showToast('已发送');
          this.smsCountDown = 60;
          this.startSMSTimer();
        }, 300);
      },
      startSMSTimer() {
        this.smsCountInterval = setInterval(() => {
          this.smsCountDown--;
          if (this.smsCountDown <= 0) {
            clearInterval(this.smsCountInterval);
          }
        }, 1000);
      },
      onSMSLogin() {
        this.onLoginClick();
      },
      // 模拟登陆
      onLoginClick() {
        this._showLoading();
        setTimeout(() => {
          this._dismissLoading();
          this.saveUserInfo();
          this._showConfirm('登陆成功, 去设置手势密码？', () => {
            this._routeReplace('GestureCreate');
          }, this._routerBack);
        }, 1000);
      },
      //保存用户信息
      saveUserInfo() {
        let info = {userName: this.userName};
        // 全局修改
        this.$store.commit('setUserInfo', info);
        // 持久化修改
        localStorage.setItem('userInfo', JSON.stringify(info));
      },
    },
  }
</script>

<style scoped>
  .send-btn {
    height: 26px;
    line-height: 24px;
  }

  .button-con {
    margin-top: 36px;
  }

  .top-area {
    margin: 30px 0;
  }

  .login-con {
    background-size: 100% 100%;
    height: calc(100vh - 46px);
  }

  .login-btn {
    width: 96%;
    margin: 12px;
  }

  .top-logo {
    height: 100px;
    width: 100px;
    margin: 16px 0;
  }
  .tabbtn{
    overflow: hidden;
    position: relative;
  }
  .tabbtn span{
    margin-top:5px ;
    font-size: 23px;
    float:right;
  }
  .tabbtn span:nth-of-type(1){
    display: inline-block;
    border-right:1px soild #333;
  }
  .res{
    font-size: 23px;
    padding-top: 10px;
  }
  .forget{
    overflow: hidden;
    position: relative;
  }
  .forget span{
    font-size: 23px;
    padding-top: 6px;
    float: right;
    padding-right: 2px;
  }
  .regTile{
    font-size: 23px;
    margin:0 auto;
    text-align:center;
  }
  .selTel{
    float: left;
  }

</style>
