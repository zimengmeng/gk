  <template>
  <section class="agents wrap">
    <Header></Header>
    <div class="agent-conten main">
        <div class="backgrounds">
                    <h1> P A R T N E R </h1>
                    <H2> G A L A X Y · K </H2>
                    <div class="mark">
                        <img src="../../../assets/img/agentStatics/logo.png" alt="">
                        <h6> {{userinfo.userAccount}}</h6>
                        <p>{{$t('public.hd.economic')}}</p>
                        <div  v-if="userinfo.inviteCode">
                            <span>{{$t('personal.invitedCode')}}:  {{userinfo.inviteCode}}</span>
                            <span class="spc"> {{inviteUrl}}<input class="inviteUrl_inp" type="text" name="url" ref="inviteUrl" :value="inviteUrl" /><a @click="copyUrl" href="javascript:void(0)" style="padding-left:20px">{{$t('personal.copyCode')}}</a></span>
                            <a @click="copyCode" href="javascript:void(0)" class="QEcode">{{$t('personal.Qecode')}}</a>
                        </div>
                    </div>
        </div>
        <div class="return">
                    <div class="title">
                        <h1>{{$t('agent.invitations')}} <span>{{$t('public.agentStatic.return')}}</span> </h1>
                        <div>
                            <p class="p">
                               <!-- 邀请总人数 -->
                               {{$t('agent.total_number')}}：<span>{{bonus.totalChild}}</span> /人
                            </p>
                            <p>
                              <!-- 有效用户 -->
                                {{$t('agent.Effective')}}：<span>{{bonus.trueChild}}</span> /人
                            </p>
                        </div>
                    </div>
                    <div class="maid">
                        <div class="cale">
                            <div class="income-con">
                                {{$t('agent.Revenue')}}{{bonus.totalBonus}}&nbsp;{{bonus.agentRoleSymbol}}
                            </div>
                            <div class="calendar">
                                  <div class="title">
                                    <b class="last-year" @click="lastYear"> &lt;&lt;</b> <i class="last-month" @click="preMonth">&lt;</i> {{year}}{{$t('agent.year')}}{{month + 1}}{{$t('agent.month')}} <i class="next-month" @click="nextMonth">&gt;</i> <b class="next-year" @click="nextYear">&gt;&gt;</b>
                                  </div>
                                  <div class="date">
                                  <div class="week">
                                    <b>{{$t('agent.sun')}}</b>
                                    <b>{{$t('agent.mon')}}</b>
                                    <b>{{$t('agent.tue')}}</b>
                                    <b>{{$t('agent.wed')}}</b>
                                    <b>{{$t('agent.thu')}}</b>
                                    <b>{{$t('agent.fri')}}</b>
                                    <b>{{$t('agent.sat')}}</b>
                                  </div>
                                  <div class="dail clearfix">
                                      <span v-for="(item,index) in list" :key="index" class="day">
                                          <b class="date" :class="{days:item.num === '&nbsp'}"  @click="getbonus(year,month,item.num,bonus.agentRoleSymbol)">{{item.num}}</b>
                                          <b class="data" :class="{days:item.num === '&nbsp'}" v-for="i in bonus.calendarBonusList" v-if="item.date === i.day" @click="getbonus(year,month,item.num,bonus.agentRoleSymbol)">{{i.amount+'GKO'}}</b>                          
                                      </span>
                                  </div>
                            </div>
                        </div>
                    </div>
        </div>
      </div>
    </div>
    <div class="projectile" v-if="project">
      <div class="expor-list">
         <table>
                <thead>
                   <tr class="title">
                    <!-- <th>UID</th> -->
                    <th>{{$t('agent.mailbox')}}</th>
                    <th>{{$t('agent.Telephone')}}</th>
                    <th>{{$t('agent.time')}}</th>
                    <th>{{$t('agent.Remaid')}}</th>
                    <th>{{$t('agent.Amount')}}</th>
                   </tr>
                  <span class="cols" @click="cols">╳</span> 
                 </thead>
                 
                 <tbody>
                   <tr v-for="(item,index) in mapList" :key="index" :class="{interlacing: index % 2 === 1}">
                     <!-- <td>{{item.uid}}</td> -->
                     <td>{{item.email}}</td>
                     <td>{{item.mobileNumber}}</td>
                     <td>{{item.ctime}}</td>
                     <td>{{item.scale}}%</td>
                     <td>{{item.amount + 'GKO'}}</td>
                   </tr>
                 </tbody>
               
              </table>
              <div v-if="mapList <=0" class="no_data">
                       {{$t('agent.nodata')}}
              </div>
              <div class="page">
                 <Vpagination v-if="(apition.count/apition.pageSize) > 1"
                              :total="apition.count"
                              :current-page='apition.page'
                              :display='apition.pageSize'
                              @pagechange="apitionechage($event)" class="page">
                 </Vpagination>
              </div>
      </div>
    </div>
    <Footer></Footer>
      <el-dialog 
                :title='tiptlText' 
                :flag='isVerifyDialog'
                name= 'isVerifyDialog'
                :width='450'
                :dialogClose='closeDialog'>
                <div class="mobileverify-text" slot="content">{{$t('personal.text_4')}}</div>
                <div slot="options">
                    <!-- this.userinfo.googleStatus === 0 && this.userinfo.isOpenMobileCheck === 0 -->
                    <template v-if="userinfo.isOpenMobileCheck === 0">
                        <button @click="openMobileVerify" v-if="userinfo.mobileNumber">{{$t('personal.openPhoneVer')}}</button>
                        <router-link  v-else :to="{path: '/personal/bindMobile'}" >
                            <button >{{$t('personal.openPhoneVer')}}</button>
                        </router-link>
                    </template>
                    <router-link :to="{path: '/personal/googlebind'}" v-if="userinfo.googleStatus === 0">
                        <button>{{$t('personal.opengoogleVer')}}</button>
                    </router-link>
                    <!-- <button>开启谷歌验证</button> -->
                </div>
      </el-dialog >
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
            <!-- 删除支付方式 短信或谷歌验证 -->
      <el-dialog 
                :title='tiptlText'
                :flag='isDeleteDialog'
                name= 'isDeleteDialog'
                :width='450'
                :dialogClose='closeDialog'>
                <div slot="content">
                    <div>
                        <template v-if="verifiFormList" v-for="(item,key,index) in verifiFormList">
                            <inline-input 
                                :property = "item"
                                v-model="item.value"
                                v-on:onevents="somethings" > 
                            </inline-input>
                        </template>
                    </div>
                </div>
                <div slot="options">
                    <button class="cancel" @click="closeDialog('isDeleteDialog')">{{$t('trade.cancel')}}</button>
                    <button @click="deletePayment()">{{$t('personal.confirm')}}</button>
                </div>
      </el-dialog >
      <p v-if="public_info"></p>
  </section>

</template>

<script lang="js">
import { mapState } from 'vuex'
import elDialog from '@/components/common/dialog'
import VPagination from '@/components/common/pagination'
import InlineInput from '@/components/common/inlineInput'
import Header from '../../module/header'
import Footer from '../../module/footer'
export default {
  name: '',
  props: [],
  components: {elDialog, VPagination, InlineInput,Header,Footer},
  mounted () {
    let nstr = new Date()
    let year = nstr.getFullYear()
    this.year = year
    let month = nstr.getMonth()
    this.month = month
    this.calendar(this.year, this.month)
    this.getData(),
//////////////////////////////////////////////////////////
    this.getHistoryData(1)
    this.$store.dispatch('getCommonUser_info')
    if (this.isotcOpen === '1') {
      this.$store.dispatch('otcPublic_info')
      this.getPaymentLIst()
    }
  },
  data () {
    return {
      year: '',   // 当前年份
      month: '',   // 当前月份
      list: [],
      bonus: '',
      project: false,
      firstFlag: true,
      baseData: [],
      mapList: '',
      mones: '',
      apition: {
        count: '',
        pageSize: 10,
        page: 1
      },
      days: '',
      id: '',
 ///////////////////////////////////
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
    computed: {
      ...mapState({
        userinfo ({baseData: {_user}}) {
        if (_user) {
          this.nickName = _user.nickName
          this.inviteQECode = _user.inviteQECode
          this.useFeeCoinOpen = _user.useFeeCoinOpen
        }
        return _user || false
      },
        public_info ({baseData}) {
        if (baseData.isReady && this.firstFlag) {
          this.baseData = baseData
          this.id = baseData._user.exportExcelAuth
          this.getData()
          this.firstFlag = false
          return baseData
        } else {
          return true
        }
      }
      }),
       Url () {
      return 'https://' + window.HOST_API.ex_api + '/agent/agent_branch_bonus_export' + '?timeStr=' + this.year + '_1_' + this.id
      // return 'http://192.168.1.241:8082/agent/agent_branch_bonus_export?timeStr=2018_1_AQTDDDVZU'
      },
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
    historyTab (type) {
      this.historyData = []
      this.historyTabClass = type
      this.pagination.page = 1
      this.getHistoryData(1)
    },
    getHistoryData (page) {
      let ajaxUrl = this.$store.state.url.question.login_history
      if (this.historyTabClass === 'setting') {
        ajaxUrl = this.$store.state.url.question.setting_history
      }
      let data = {
        page: page,
        pageSize: 10,
        userId: this.userinfo.id
      }
      this.axios({
        url: ajaxUrl,
        headers: {},
        params: data,
        method: 'post'
      }).then((data) => {
        if (data.code.toString() === '0') {
          let dataList
          this.pagination.count = data.data.count
          if (this.historyTabClass === 'setting') {
            dataList = data.data.historySettingList
          } else {
            dataList = data.data.historyLoginList
          }
          this.historyData = dataList
        }
      })
    },
    // 翻页点击事件
    pagechange (page) {
      this.pagination.page = page
      this.getHistoryData(page)
    },

    Admini () {
      this.$router.push({path: '/agent'})
    },

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

calendar (year, month) {
      let lastday = new Date(year, month, 1)   // 当前月第一天
      let firstday = lastday.getDay()              // 当前月第一天周几
      let mdays = [31, 28 + this.leap(year), 31, 30, 31, 31, 30, 31, 30, 31, 30, 31]
      let trstr = Math.ceil((mdays[month] + firstday) / 7)
      for (let i = 0; i < trstr; i++) {
        for (let k = 0; k < 7; k++) {
          let idx = i * 7 + k
          let datestr = idx - firstday + 1 // 计算日期
          let datestrs = {}
          if (datestr <= 0 || datestr > mdays[month]) {
            datestrs.num = '&nbsp'
          } else {
            let num = idx - firstday + 1
            datestrs.num = num
            datestrs.date = this.year + '-' + this.s(this.month + 1) + '-' + this.s(num)
          }
          this.list.push(datestrs)
        }
      }
    },
      // 上一年
    lastYear () {
      this.year = this.year - 1
      this.list = []
      this.getData()
      this.calendar(this.year, this.month)
    },
      // 下一年
    nextYear () {
      this.year = this.year + 1
      this.list = []
      this.getData()
      this.calendar(this.year, this.month)
    },
      // 上一个月
    preMonth () {
      if (this.month <= 0) {
        this.year = this.year - 1
        this.month = 11
        this.list = []
        this.getData()
        this.calendar(this.year, this.month)
      } else {
        this.month --
        this.list = []
        this.getData()
        this.calendar(this.year, this.month)
      }
    },
      // 下一个月
    nextMonth () {
      if (this.month >= 11) {
        this.year = this.year + 1
        this.month = 0
        this.list = []
        this.getData()
        this.calendar(this.year, this.month)
      } else {
        this.month ++
        this.list = []
        this.getData()
        this.calendar(this.year, this.month)
      }
    },
    leap (year) {  // 判断是否为闰年
      return (((year % 4 === 0) && ((year % 100) !== 0)) || (year % 400 === 0))
    },
    getData () {
      this.axios({
        url: this.$store.state.url.bonus.calendar_bonus,
        headers: {},
        params: {
          currentMonthStr: this.Time(new Date())
        },
        method: 'post'
      }).then((data) => {
        if (data.code === '0') {
          let boun = data.data 
          boun.totalBonus = this._P.fixD(boun.totalBonus, this.baseData._coinList[boun.agentRoleSymbol].showPrecision)
          for (let i in boun.calendarBonusList) {
            boun.calendarBonusList[i].amount = this._P.fixD(boun.calendarBonusList[i].amount, this.baseData._coinList[boun.agentRoleSymbol].showPrecision)
            boun.calendarBonusList[i].day = this.Time(boun.calendarBonusList[i].ctime)
          }
          this.symbol = boun.agentRoleSymbol
          this.bonus = boun
        } else {
          this.$store.dispatch('setTipState', {text: data.msg, type: 'error'})
        }
      })
    },
    getbonus (year, month, day, symbol) {
      this.days = day
      let date = year + '-' + this.s(month + 1) + '-' + this.s(day)
      this.axios({
        url: this.$store.state.url.bonus.bonus_record,
        headers: {},
        params: {
          currentDateStr: date,
          pageNumber: this.apition.page,
          pageSize: this.apition.pageSize

        },
        method: 'post'
      }).then((data) => {
        if (data.code === '0') {
          this.project = true
          let mapList = data.data.mapList
          for (let item in mapList) {
            mapList[item].ctime = this._P.formatTime(mapList[item].ctime)
            mapList[item].amount = this._P.fixD(mapList[item].amount, this.baseData._coinList[symbol].showPrecision)
          }
          this.apition.count = data.data.count
          this.mapList = mapList
        } else {
          this.$store.dispatch('setTipState', {text: data.msg, type: 'error'})
        }
      })
    },
    Time: function (dateTime) {
      let date = new Date(dateTime)
      let year = date.getFullYear()
      let month = date.getMonth() + 1
      let day = date.getDate()
      return year + '-' + this.s(month) + '-' + this.s(day)
    },
    s (t) {
      return t < 10 ? '0' + t : t
    },
      // 关闭弹框
    cols () {
      this.project = false
      this.apition.page = 1
    },
    apitionechage (i) {
      this.apition.page = i
      this.getbonus(this.year, this.month, this.days, this.symbol)
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
}
</script>

<style scoped>
.wrap{
    width: 100%;
    height: 100%;
    background: #030E20;
    margin: 0;
    padding: 0;
}
.detail{
    width: 100%;
    background: #030E20;
    margin: 0 auto;
}
.main{
    width: 1200px;
    margin: 0 auto;
    text-align: center;
}
.backgrounds{
    width: 100%;
    height: 600px;
    position: relative;
    background: #030E20;
}
.backgrounds h1{
    width: 100%;
    height: 350px;
    box-sizing: border-box;
    padding-top:150px; 
    font-size: 140px;
    color:#101A2B;
}
.backgrounds h2{
    width: 100%;
    height: 210px;
    font-size: 70px;
    color:#101A2B;
}
.backgrounds .mark{
    width: 765px;
    height: 355px;
    position: absolute;
    top: 205px;
    left: 215px;
}
.backgrounds .mark img{
    width: 80px;
    height: 80px;
}
.backgrounds .mark h6{
    font-size: 16px;
    color: #fff;
    line-height: 70px;
}
.backgrounds .mark p{
    color: #777;
}
.backgrounds .mark div{
    width: 100%;
    height: 180px;
    box-sizing: border-box;
    padding: 65px 0 100px 0;
    display: flex;
    justify-content: space-between;
}
.backgrounds .mark div span{
    font-size: 12px;
    color: #fff;
}
.backgrounds .mark div .spc{
    font-size: 12px;
    color: #777;
}
.backgrounds .mark div .spc a{
    font-size: 12px;
    color: #fff;
}
.return{
    width: 100%;
    background: #030E20;
 }
.return .title{
    width: 1000px;
    height: 40px;
    line-height:40px;
    margin: 0 auto;
}
.return .title h1{
    float: left;
    font-size: 24px;
    color: #fff;
}
.return .title h1 span{
  font-size: 14px;
  color: #777;
}
.return .title div{
    width: 300px;
    float: right;
    font-size: 14px;
    color: #fff;
}
.return .title div .p{
  float: right;
  display: block;
}
.return .cale{
   width: 100%;
   border: 2px solid #2F3E57;
   background: #101A2B;
}
.agents .agent-conten .maid .cale{
  margin-top: 10px;
}
.return .cale .income-con{
  width: 100%;
  line-height: 90px;
  font-size: 14px;
  color: #fff;
}
.return .cale .calendar{
  margin: 0;
  border: 0;
}
.return .cale .calendar .title{
  width: 100%;
  padding: 0;
  height: 60px;
  line-height: 60px;
}
.return .cale .calendar .title b{
  box-sizing: border-box;
  padding: 0 0 0 300px;
}
.return .cale .calendar .title .next-year{
  box-sizing: border-box;
  padding: 0 300px 0 0;
}
  .inviteUrl_inp {
    position: absolute;
    top: -9999px;
    left: -9999px;
    opacity: 0;
  }
  .day{
    /* line-height: 30px; */
  }
  .mobileverify-text {
    text-align: center;
    padding-top: 10px;
    font-size: 16px;
  }
  .QEcode{
      color: #fff;
  }
  .qeCode{
    display: block;
    margin: 0 auto;
  }
</style>