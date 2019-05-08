<template>
    <div class="wrap">
        <Header></Header>
        <div class="agentStatic">
           <div class="main">
                <div class="partner">
                    <dl>
                        <dt>
                            <img src="../../assets/img/agentStatics/img_partner.png" alt="">
                        </dt>
                        <dd>
                            <h1>{{$t('public.agentStatic.super')}}</h1>
                            <span></span>
                            <p>{{$t('public.agentStatic.quotas')}}</p>
                        </dd>
                    </dl>
                </div>
                <div class="title">
                    <h6>{{$t('public.agentStatic.platform')}}</h6>
                    <p>{{$t('public.agentStatic.mode')}}</p>
                    <p>{{$t('public.agentStatic.becoming')}}</p>
                    <h6>{{$t('public.agentStatic.money')}}</h6>
                    <div class="super" v-if="userinfo.agentStatus!==1">
                        <a class="apply" href="https://jinshuju.net/f/DDNT30" target="_blank">{{$t('public.agentStatic.apply')}}</a>
                    </div>
                    <div class="code" v-if="userinfo.agentStatus===1">
                        <div class="codes"  v-if="userinfo.inviteCode">
                            <span>{{$t('personal.invitedCode')}}:  {{userinfo.inviteCode}}</span>
                            <span class="spc"> {{inviteUrl}}<input class="inviteUrl_inp" type="text" name="url" ref="inviteUrl" :value="inviteUrl" /><a @click="copyUrl" href="javascript:void(0)" style="padding-left:20px">{{$t('personal.copyCode')}}</a></span>
                            <a @click="copyCode" href="javascript:void(0)" class="QEcode">{{$t('personal.Qecode')}}</a>
                        </div>
                         <div class="return" @click="clicks">
                            <router-link to="/agent">{{$t('public.agentStatic.check')}}</router-link>
                        </div> 
                    </div>
                   
                </div>
                <div class="maid">
                    <h1>{{$t('public.agentStatic.award')}}</h1>
                    <p>{{$t('public.agentStatic.enjoy')}}</p>
                    <ul>
                        <li>
                            <div class="one">
                                <img src="../../assets/img/agentStatics/img_diamonds_yellow.png" alt="">
                                <span>30<font>%</font></span>
                            </div>
                            <p> {{$t('public.agentStatic.first')}}</p>
                        </li>
                        <li class="spc">
                            <div class="two">
                               <img src="../../assets/img/agentStatics/img_diamonds_blue.png" alt="">
                               <span> 15<font>%</font></span>
                            </div>
                            <p>{{$t('public.agentStatic.two')}}</p>
                        </li>
                        <li>
                            <div class="three">
                                <img src="../../assets/img/agentStatics/img_diamonds_red.png" alt="">    
                                <span>10<font>%</font> </span>
                            </div>
                            <p> {{$t('public.agentStatic.three')}}</p>
                        </li>
                    </ul>
                </div>
                <div class="need">
                    <h1>{{$t('public.agentStatic.requirements')}}</h1>
                    <ul>
                        <li>
                            <img src="../../assets/img/agentStatics/img_select01.png" alt="">
                            <p>{{$t('public.agentStatic.independently')}}</p>
                        </li>
                         <li>
                            <img src="../../assets/img/agentStatics/img_select02.png" alt="">
                            <p>{{$t('public.agentStatic.rich')}}</p>
                        </li>
                         <li>
                            <img src="../../assets/img/agentStatics/img_select03.png" alt="">
                            <p>{{$t('public.agentStatic.block')}}</p>
                        </li>
                         <li>
                            <img src="../../assets/img/agentStatics/img_select04.png" alt="">
                            <p>{{$t('public.agentStatic.engaging')}}</p>
                        </li>
                    </ul>
                </div>
           </div>
        </div>
        <Footer></Footer>
      <el-dialog 
                :title='Qecode'
                :flag='copyShow'
                name= 'copyShow'
                :width='450'
                :dialogClose='closeDialog'>
                <div slot="content">
                    <img :src="inviteQECode" class="qeCode">
                </div>
                <div slot="options">
                    <button @click="closeQC">{{$t('personal.confirm')}}</button>
                </div>
      </el-dialog >
    </div>
</template>
<script>
    // clicks
import { mapState } from 'vuex'
import elDialog from '@/components/common/dialog'
import VPagination from '@/components/common/pagination'
import InlineInput from '@/components/common/inlineInput'
import Header from '../module/header.vue'
import Footer from '../module/footer.vue'
export default {
  name: 'personal',
  props: [],
  components: {elDialog, VPagination, InlineInput,Header,Footer},
  data () {
    return {
      editNickNameStatus: false,
      closeMobileVerifyDialog: false,
      isVerifyDialog: false,
      useFeeCoinOpen: 0,
      historyTabClass: 'login',
      historyData: [],
      nickName: null,
      inviteQECode: null,
      copyShow: false,
      pagination: {
        count: 0,
        page: 1,
        display: 10
      },
      isotcOpen: this.$store.state.baseData.otcOpen,
      isDeleteDialog: false,
      deletePaymentData: null,
      deletePaymentIndex: null,
      paymentLIst: [],
      verifiFormList: {},
      deleteFla: true
    }
  },
  mounted () {
    this.$store.dispatch('getCommonUser_info')
    if (this.isotcOpen === '1') {
      this.$store.dispatch('otcPublic_info')
      this.getPaymentLIst()
    }
  },
  watch: {
    'verifiFormList_obj' (value) {
      this.verifiFormList = value
    },
    '$store.state.baseData.otcOpen' (value) {
      this.isotcOpen = value
      if (value === '1') {
        this.$store.dispatch('otcPublic_info')
        this.getPaymentLIst()
      }
    }
  },
  computed: {
    ...mapState({
      userinfo ({baseData: {_user}}) {
        if (_user) {
          this.nickName = _user.nickName
          this.inviteQECode = _user.inviteQECode
          this.useFeeCoinOpen = _user.useFeeCoinOpen
        }
        return _user || false
      }
    }),
    // 删除 收款方式 的验证码input
    verifiFormList_obj () {
      let obj = {}
      // 短信验证码
      if (this.userinfo.isOpenMobileCheck === 1) {
        obj.smsAuthCode = {
          title: this.$t('personal.smsAuthCode'),
          formType: 'verifiCode',
          name: 'smsAuthCode',
          operationType: 28,
          placeholder: this.$t('personal.text_7') + this.$t('personal.smsAuthCode'), // 请输入短信验证码
          startTime: false,
          data: [],
          value: null
        }
      }
      // google 验证码
      if (this.userinfo.googleStatus === 1) {
        obj.googleCode = {
          title: this.$t('personal.googleCode'),
          placeholder: this.$t('personal.text_7') + this.$t('personal.googleCode'), // 请输入谷歌验证码
          formType: 'number',
          type: null,
          name: 'googleCode',
          value: null
        }
      }
      return obj
    },
    // 邀请链接
    inviteUrl () {
      // return location.origin + '/register?inviteCode=' + this.userinfo.inviteCode
      return window.HOST_API.ex_pc_url + '/register?inviteCode=' + this.userinfo.inviteCode
    },
    // 邀请二维码
    Qecode () {
      return this.$t('personal.Qecode')
    },
    tiptlText () {
      return this.$t('personal.tiptl')
    },
    text () {
      return {
        editNameBtn: this.$t('personal.edit')
      }
    }
  },
  methods: {
    clicks(){
        this.$router.push({ name: 'agent' })
    },
    somethings (data) {
      if (data.handleType === 'sendCode') {
        this.sendCode(data)
      }
    },
    closeDialog (e) {
      this[e] = false
      if (this.userinfo.isOpenMobileCheck === 1) {
        this.verifiFormList_obj['smsAuthCode'].startTime = false // 关闭短信验证码的倒计时
        this.verifiFormList_obj['smsAuthCode'].value = ''
      }
      if (this.userinfo.googleStatus === 1) {
        this.verifiFormList_obj['googleCode'].value = ''
      }
    },
    closeQC () {
      this.copyShow = false
    },
    // 复制链接
    copyUrl () {
      this.$refs.inviteUrl.select()
      document.execCommand('copy')
      this.$store.dispatch('setTipState', this.$t('personal.copeSuccess'))
    },
    copyCode () {
      this.copyShow = true
    },
  }
}
</script>
<style scoped>
.wrap{
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
}
.agentStatic{
    width: 100%;
    height: 1900px;
    background: #030e20;
    margin: 0 auto;
}
.main{
    width: 1210px;
    height: 100%;
    margin: 0 auto;
}
 .partner{
    width: 100%;
    height: 480px;
    box-sizing: border-box;
    padding-top:88px; 
}
.partner dl{
    width: 100%;
    height: 100%;
    margin: 0 auto;
    text-align: center;
}
.partner dl dt{
    width: 430px;
    height: 225px;
    margin: 0 auto;
}
.partner dl dt img{
    width: 100%;
    height: 100%;
}
.partner dl dd h1{
    font-size: 60px;
    box-sizing: border-box;
    padding: 18px 0;
    color: #a28928;
}
.partner dl dd span{
    display: inline-block;
    width: 90px;
    border-top: 2px solid #ffca10;
}
.partner dl dd p{
    font-size: 26px;
    line-height:58px;
    color: #ffca10;
}
.title{
    width: 100%;
    height: 600px;
    text-align: center;
}
.title h6{
    font-size: 14px;
    color: #777;
    line-height: 80px;
}
.title p{
    font-size: 14px;
    color: #777;
    line-height: 20px;
}
.title .super{
    box-sizing: border-box;
    padding: 40px 0;
}
.title .super .apply{
    text-decoration: none;
    display: inline-block;
    width: 220px;
    height: 60px;
    background: #ffca10;
    color: #030e20;
    line-height: 60px;
    text-align: center;
    font-size: 20px;
    border-radius: 30px;
    cursor: pointer;
}

.title .return{
    width: 100%;
}
.title .return a{
    text-decoration: none;
    display: inline-block;
    width: 220px;
    height: 60px;
    background: #ffca10;
    color: #030e20;
    line-height: 60px;
    text-align: center;
    font-size: 14px;
    border-radius: 30px;
    cursor: pointer;
}
.title .return span{
    display: inline-block;
    width: 0px;
    height: 0px;
    border-width: 4px;
    border-style: solid;
    border-color: transparent transparent transparent #fff;
    box-sizing: border-box;
}
.title .code .codes{
    width: 100%;
    height: 100px;
    line-height: 100px;
    border: 2px solid #2F3E57;
    margin-bottom: 50px;
    box-sizing: border-box;
    padding: 0 100px;
    display: flex;
    justify-content: space-between;
}
.maid{
    width: 100%;
    height: 450px;
    text-align: center;
}
.maid h1{
    font-size: 26px;
    color: #fff;
    line-height: 72px;
}
.maid p{
    font-size: 14px;
    color: #777;
}
.maid ul{
    width: 100%;
    height: 360px;
    box-sizing: border-box;
    padding:40px 0 140px 0;
    float: left; 
}
.maid ul li{
    width: 378px;
    height:200px;
    border: 1px solid #102341;
    float: left; 
    background: #010A17;
}
.maid ul .spc{
    margin:0 35px 0 35px;
}
.maid ul li div{
    width: 100%;
    height: 120px;
    box-sizing: border-box;
    padding:26px 0 20px 0;
    position: relative;
}
.maid ul li div img{
    width:94px;
    height:96px;
}
.maid ul li div span{
   display: inline-block;
   position: absolute;
   left: 170px;
   bottom: 20px;
   font-size: 26px;
   color: #030E20;
}
.maid ul li div span font{
   font-size: 12px;
   color: #030E20;
}
.maid ul .spc div span{
    left: 155px;
   bottom: 20px;
}
.maid ul li p{
    line-height: 45px;
    font-size: 12px;
    color: #fff;
}
.need{
    width: 100%;
    height: 450px;
    text-align: center;
}
.need h1{
    font-size: 26px;
    color: #fff;
    line-height: 114px;
}

.need ul{
    width: 100%;
    box-sizing: border-box;
    padding:40px 0 140px 0;
    float: left; 
}
.need ul li{
    width:285px;
    height:60px;
    border: 1px solid #102341;
    float: left; 
    background: #010A17;
    vertical-align: middle;
    margin:0 5px;
    position: relative;
}
.need ul li img{
    width: 34px;
    height: 34px;
    float: left;
    position: absolute;
    left: 10px;
    top: 13px;
}
.need ul li p{
    width:336px;
    font-size: 12px;
    color: #fff;
    line-height: 60px;
}
  .inviteUrl_inp {
    position: absolute;
    top: -9999px;
    left: -9999px;
    opacity: 0;
  }
    .qeCode{
    display: block;
    margin: 0 auto;
  }
</style>

