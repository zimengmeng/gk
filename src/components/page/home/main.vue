<template>
  <div class="m-main bg-color font-color" > 
    <Header class="header"></Header>
  <!-- 轮播 -->
    <!-- <div class="carousel">
      <div class="slide-img">
        <template v-if="sildePage.length > 1">
          <slider :pages="sildePage" :sliderinit="sliderinit" @tap='onTap'></slider>
        </template>
        默认显示图片
        <div v-else>
          <div v-if="sildePage.length === 1" v-html="sildePage[0].html"></div>
        </div>
      </div>
      轮播end
    </div> -->


    
    <div class="main-content">
      <!-- <div class="noticeBox" id="noticeBox"> -->
        <!-- <i class="horn icon-broadcast"></i> 11111 -->
        <!-- <template v-if="noticeInfoList.length > 1">
          <slider :pages="noticeInfoList" :sliderinit="noticeinit" @tap='noticesOnTap'></slider> 
          <div class="noticeSmallBox">
            <ul>
              <li v-for="(item, index) in noticeInfoList" :key="index">{{item.html}}</li>
            </ul>
          </div>
        </template>
        <template v-else>
          <p class="notice" v-if="notice" @click="notices(notice.id)">{{notice.title}}</p>
        </template> -->
        <!-- <p @click="notices(notice.id)" class="notices_more">{{this.$t('main.more')}}></p> 11111-->
      <!-- </div>  -->
      <!-- <ul class="siteTab clearfix" v-if="itemArray.length > 1">
        <li v-for="(item, index) in itemArray"
            :key='index'
            :class="{selected: currentItem === item}" 
            @click="switchItem(item)">
          {{itemArrayText[index].text}}
        </li>
      </ul> -->
      <template v-for="(item, index) in itemArray">
        <div :key='index'>
          <div v-if="item === 'ex'">
            <!-- 交易所市场 -->
            <market-ex v-show="currentItem === 'ex'"></market-ex>
          </div>
          <div v-if="item === 'otc'">
            <!-- 场外市场 -->
            <market-otc v-show="currentItem === 'otc'"></market-otc>
          </div>
          <div v-if="item === 'co'">
            <!-- 合约市场 -->
            <market-co v-show="currentItem === 'co'"/>
            <!-- <market-otc v-show="currentItem === 'otc'"></market-otc> -->
          </div>
        </div>
      </template>
      <!-- <market-co></market-co> -->
      
      <div class="prompt">
      <b>{{prompt}}</b>
      </div>
    </div>
    <p v-if="!public_info"></p>
    <Footer class="footer"></Footer>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import Header from '../../module/header'
import Footer from '../../module/footer'
import slider from 'vue-concise-slider'// 引入slider组件
import marketEx from './ex.vue'// 引入交易所的首页
import marketOtc from './otc.vue'// 引入场外的首页
import marketCo from './co.vue'// 引入场外的首页
export default {
  name: 'm-main',
  components: {
    slider,
    marketEx,
    marketOtc,
    marketCo,
    Header,
    Footer
  },
  data () {
    return {
      firstFlag: null,
      baseData: {},
      sildePage: [],
      isArr: [], // 轮播图数据
      mack: 0,   // 图片索引
      time: null, // 定时器
      notice: null,  // 公告
      sliderinit: {
        currentPage: 0,
        thresholdDistance: 500,
        thresholdTime: 100,
        autoplay: 10000,
        loop: true,
        infinite: 1,
        slidesToScroll: 1,
        timingFunction: 'ease',
        duration: 300
      },
      noticeinit: {
        pagination: false,
        currentPage: 0,
        thresholdDistance: 500,
        thresholdTime: 100,
        autoplay: 6000,
        loop: true,
        direction: 'vertical',
        infinite: 1,
        slidesToScroll: 1,
        timingFunction: 'ease',
        duration: 300
      },
      noticeInfoList: [],
      noticeList: [],
      host: this.$store.state.baseData._webSiteInfo,
      prompt: this.$store.state.baseData.prompt,
      itemArray: [],
      currentItem: null,
      moreSite: false,
      myMarket: localStorage.getItem('myMarket')
        ? localStorage.getItem('myMarket').split(',')
        : []
    }
  },
  mounted () {
    this.getLundata()
    // if (this.host.ex_open === '1') {
    //   this.itemArray.push('ex')
    // }
    // if (this.host.otc_open === '1') {
    //   this.itemArray.push('otc')
    // }
    // if (this.host.co_open === '1') {
    //   this.itemArray.push('co')
    // }
    // if (!this.itemArray.length) {
    let siteType = window.siteType || ['ex']
    this.itemArray = siteType
    // }
    this.currentItem = this.itemArray[0]
  },
  computed: {
    ...mapState({
      public_info ({baseData}) {
        if (baseData.isReady && this.firstFlag) {
          this.baseData = baseData
          this.prompt = baseData.prompt
          this.firstFlag = false
          return true
        } else {
          return true
        }
      }
    }),
    itemArrayText () {
      return [
        {
          text: '币币市场',
          val: 'ex'
        },
        {
          text: '场外市场',
          val: 'otc'
        },
        {
          text: '合约市场',
          val: 'co'
        }
      ]
    }
  },
  watch: {
    // 监听 语言切换
    '$store.state.baseData._lan' (val, old) {
      // 重新请求轮播图
      if (old) {
        this.getLundata()
      }
    },
    '$store.state.baseData.prompt' (val) {
      this.prompt = val
    }
  },
  methods: {
    notices (i) {
      localStorage.setItem('ntId', i)
      this.$router.push({name: 'notice_info', query: { ntId: i }})
    },
    // 切换Tab
    switchItem (type) {
      this.currentItem = type
    },
    getLundata () {
      this.axios({
        url: this.$store.state.url.common.index_data,
        headers: {},
        params: {},
        method: 'post'
      }).then((data) => {
        if (data.code === '0') {
          if (data.data.noticeInfoList && data.data.noticeInfoList.length > 0) {
            this.noticeList = data.data.noticeInfoList
            let noticearr = []
            for (let j = 0; j < this.noticeList.length; j++) {
              let noticeObj = {}
              noticeObj.html = this.noticeList[j].title
              noticearr.push(noticeObj)
            }
            this.noticeInfoList = noticearr
          }
          this.notice = data.data.noticeInfo
          let res = data.data.cmsAdvertList
          this.isArr = []
          let arr = []
          for (let i = 0; i < res.length; i++) {
            let obj = {}
            obj.html = '<div><a target="_blank" href="' + res[i].httpUrl + '"><img src="' + res[i].imageUrl + '"></a></div>'
            arr.push(obj)
            this.isArr.push(res[i])
          }
          this.sildePage = arr
        } else {
          this.$store.dispatch('setTipState', {text: data.msg, type: 'error'})
        }
      })
    },
    onTap (data) {
      window.open(this.isArr[data.currentPage].httpUrl)
    },
    noticesOnTap (data) {
      let id = this.noticeList[data.currentPage].id
      localStorage.setItem('ntId', id)
      this.$router.push({name: 'notice_info', query: { ntId: id }})
    }
  }
}
</script>
<style scoped>
.footer{
  background: #030215;
}
</style>
