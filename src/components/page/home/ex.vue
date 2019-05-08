<template>
      <div>
         <!-- 推荐区 -->
         <div class="recommend clearfix">
          <!-- <div v-if="JSON.stringify(symbolTop) == '{}'">
            <div v-for="(item,index) in 5" class="recomm-content borderbox" :key="index"></div>
          </div> -->
           <div class="recomm-content borderbox" v-for="(item, index) in symbolListArrs" :key="index" v-if="symbolListArrs.length > 0">
             <div class="content">
                <div class="symbol_buy clearfix" @click="transaction(item.symbol)"> 
                  <span>{{item.symbol}}</span> 
                  <b :class="item.rose.class">{{item.rose.data}}</b>
                </div>
                <p class="price" :class="item.close.class">{{item.close.data}}</p>
                <span class="turnover">{{$t('main.deal_forehead')}}：{{item.amount}}&nbsp;{{item.symbolname}} </span>
             </div>
           </div>
          </div>
           <!-- 轮播 -->
          <div class="carousel">
            <div class="slide-img">
              <template v-if="sildePage.length > 1">
                <slider :pages="sildePage" :sliderinit="sliderinit" @tap='onTap'></slider>
              </template>
              <!-- 默认显示图片 -->
              <div v-else>
                <div v-if="sildePage.length === 1" v-html="sildePage[0].html"></div>
              </div>
            </div>
            <!-- 轮播end -->
          </div>
          <div class="dubble">
            <div class="dubbles">
              <div class="left">
                <div class="top">
                  <h6>{{this.$t('public.hd.pingji')}}</h6>
                   <router-link to="/dubble">{{this.$t('public.home.search')}}</router-link><span></span>
                </div>
                <div class="center">
                    <dl>
                      <dt>
                        <img src="../../../assets/img/index/1.jpg" alt="">
                      </dt>
                      <dd>
                        <h6>{{this.$t('public.home.grade')}}</h6>
                        <p>{{this.$t('public.home.grades')}}</p>
                      </dd>
                    </dl>
                     <dl>
                      <dt>
                        <img src="../../../assets/img/index/2.jpg" alt="">
                      </dt>
                      <dd>
                        <h6>{{this.$t('public.home.userRating')}}</h6>
                        <p>{{this.$t('public.home.userRatings')}}</p>
                      </dd>
                    </dl>
                </div>
              </div>
              <div class="right">
                <div class="top">
                    <h6>{{ this.$t('public.hd.gongju')}}</h6>
                    <router-link to="/lianghua">{{this.$t('public.home.search')}}</router-link><span></span>
                </div>
                <div class="center">
                  <ul>
                      <li>
                        <dl>
                    <dt>
                      <img src="../../../assets/img/index/3.jpg" alt="">
                    </dt>
                    <dd>
                      <h6>{{this.$t('public.home.deploy')}}</h6>
                      <p>{{this.$t('public.home.deploys')}}</p>
                    </dd>
                  </dl>
                  <dl>
                    <dt>
                      <img src="../../../assets/img/index/5.jpg" alt="">
                    </dt>
                    <dd>
                      <h6>{{this.$t('public.home.private')}}</h6>
                      <p>{{this.$t('public.home.privates')}}</p>
                    </dd>
                  </dl>
                  
                      </li>
                      <li>
                    <dl>
                    <dt>
                      <img src="../../../assets/img/index/4.jpg" alt="">
                    </dt>
                    <dd>
                      <h6>{{this.$t('public.home.circulation')}}</h6>
                      <p>{{this.$t('public.home.circulations')}}</p>
                    </dd>
                  </dl>
                  <dl>
                    <dt>
                      <img src="../../../assets/img/index/6.jpg" alt="">
                    </dt>
                    <dd>
                      <h6>{{this.$t('public.home.light')}}</h6>
                      <p>{{this.$t('public.home.lights')}}</p>
                    </dd>
                  </dl>

                      </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
         <!-- 一条 -->
          <div class="noticeBox" id="noticeBox">
          <!-- <i class="horn icon-broadcast"></i> -->
          <template v-if="noticeInfoList.length > 1">
          <slider :pages="noticeInfoList" :sliderinit="noticeinit" @tap='noticesOnTap'></slider> 
          <div class="noticeSmallBox">
            <ul>
              <li v-for="(item, index) in noticeInfoList" :key="index">{{item.html=item.html.slice(0,15)}}</li>
            </ul>
          </div>
        </template>
        <template v-else>
          <p class="notice" v-if="notice" @click="notices(notice.id)">{{notice.title}}</p>
        </template>
          </div> 
         <!--币对市场-->
         <div class="market front-color">
           <div class="marketBox">
            <div class="header">
               <ul>
                 <li v-for="(value,key,index) in baseData._symbols" 
                     v-if ="(key !== 'myMarket')" 
                     :key="index" @click="tabTog(key)"
                     :class='{findactive:key === markTitle}' 
                     class="coin_currency">
                    <span>
                      <template v-if="baseData._coinList[key]">
                        <img :src="baseData._coinList[key].icon" v-if="baseData._coinList[key].icon">
                      </template>
                      <img src="@/assets/img/coindef.png" v-else>
                      {{key}}
                    </span>
                  </li>
                  <li :class="{findactive:'myMarket' === markTitle}" @click="tabTog('myMarket')">
                  <span>
                    <i class="icon-store" v-if="'myMarket' === markTitle"></i> 
                    <i class="icon-cor icon-store" v-else ></i>
                    {{$t('main.marketSet')}}
                  </span>
                  </li>
              </ul>
              <div class="inputBox">
                <div class="search" :class="{active:frame}"><i class="sos icon-search"></i> <input type="text" placeholder="币种搜索:(如BTC、ETH)" v-model="search" @focus="issue" @blur="lose"> </div>
              </div>
            </div>
            <div class="mark-box">
                  <!-- <happy-scroll color="rgba(0,0,0,0.5)" size="5">   -->
                    <div>
                        <ul class="noHover">
                          <li class="market_title">{{this.$t('main.market')}}</li>
                          <li @click="marketSort('close')" class="new_price newprice_align">{{this.$t('main.close')}}
                            <span class="receet"> <i class="sorte up  iconNoFont-sup" :class="{cur: sortType === 'down'}"></i><i class="sorte down iconNoFont-sdow"  :class="{cur: sortType === 'up'}"></i></span></li>
                          <li>{{this.$t('main.height')}}</li>
                          <li>{{this.$t('main.low')}}</li>
                          <li @click="marketSor('rose')" class="rise">{{this.$t('main.rose')}} <span class="receet"> <i class="sorte up iconNoFont-sup" :class="{curr: sortType === 'dow'}"></i>   <i class="sorte down iconNoFont-sdow" :class="{curr: sortType === 'ups'}"></i></span></li>
                          <li>24H{{this.$t('main.vol')}}</li>
                          <li>24{{this.$t('main.amount')}}</li>
                          <li>信用评级</li>
                        </ul>
                    </div>
                    <div v-if="symbolListArr.length > 0">
                      <ul v-for="(item, index) in symbolListArr" v-if="item.isShow" :key="index" class="symboy_bgc">
                          <li class="mark" style="font-size:14px;color:#000;">
                            <i :class="{findactive:myMarket.indexOf(item.symbol) > -1}" class="icon-store" v-if="myMarket.indexOf(item.symbol) > -1 "  @click="changeMysymbol(item.symbol)" ></i> 
                            <i class="icon-cor icon-store"  @click="changeMysymbol(item.symbol)"  v-else></i>
                            <span @click="transaction(item.symbol)">{{item.symbol}}</span>
                          </li>
                          <li :class="item.close.class" class="newprice_align" style="font-size:12px;color:#333;">{{item.close.data}}</li>
                          <li style="font-size:12px;color:#333;">{{item.high}}&nbsp;{{item.coin}} </li>
                          <li style="font-size:12px;color:#333;">{{item.low}}&nbsp;{{item.coin}}</li>
                          <li style="font-size:12px;" :class="item.rose.class">{{item.rose.data}} </li>
                          <li style="font-size:12px;color:#333;">{{item.vol}}&nbsp;{{item.symbolname}}</li>
                          <li style="font-size:12px;color:#333;">{{item.amount}}&nbsp;{{item.coin}}</li>
                          <li v-if="item.symbol==='BTC/USDT'">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                          </li>
                          <li v-else-if="item.symbol==='ETH/USDT'||item.symbol==='ETH/BTC'">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                          </li>
                          <li v-else-if="item.symbol==='EOS/USDT'||item.symbol==='EOS/BTC'||item.symbol==='EOS/ETH'||item.symbol==='ETC/USDT'||item.symbol==='ETC/BTC'||item.symbol==='XRP/USDT'||item.symbol==='XRP/BTC'||item.symbol==='LTC/BTC'||item.symbol==='LTC/USDT'">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx2.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                          </li>
                          <li v-else>
                            <img src="../../../assets/img/index/xx1.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                            <img src="../../../assets/img/index/xx1.png" alt="">
                          </li>
                      </ul>
                    </div>
                  <!-- </happy-scroll> -->
            </div>
          </div>
         </div>
        <p v-if="!public_info"></p>
        <!-- <div class="advantage">
          <ul>
            <li>
                  <div style=" padding: 20px;; overflow: hidden;">
                    <div style=" height: 320px;">
                        <span><img src="../../../assets/img/index/youshi_icon.png"></span>
                        <p>{{this.$t('main.advantage.title1')}}</p>
                        <i>{{this.$t('main.advantage.content1')}}</i>
                    </div>
                </div>
            </li>
            <li>
                  <div style=" padding: 20px;; overflow: hidden;">
                    <div style=" height: 320px;">
                  <span><img src="../../../assets/img/index/anquan_icon.png"></span>
                  <p>{{this.$t('main.advantage.title2')}}</p>
                  <i>{{this.$t('main.advantage.content2')}}</i>
                  </div>
                </div>
            </li>
            <li>
                  <div style=" padding: 20px;; overflow: hidden;">
                    <div style=" height: 320px;">
                  <span><img src="../../../assets/img/index/shengtaiyoushi_icon.png"></span>
                  <p>{{this.$t('main.advantage.title3')}}</p>
                  <i>{{this.$t('main.advantage.content3')}}</i>
                  </div>
                </div>
            </li>
          </ul>
        </div>
        <div class="cooperation">
           <p>{{this.$t('main.partners')}}</p>
          <font>{{this.$t('main.zhichi')}}</font>
          <ul>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006194959841.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202307288.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202327310.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202348369.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202406667.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202429344.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202446673.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202506436.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181010205505966.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202542822.png"></li>
              <li><img src="../../../assets/img/index/par/elven_icon.png"></li>
              <li><img src="../../../assets/img/index/par/twele_icon.png"></li>
          </ul>
        </div>
        <div class="cooperation">
           <p>{{this.$t('main.meiti')}}</p>
           <font>{{this.$t('main.zhichi')}}</font>
          <ul>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006194959841.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202307288.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202327310.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202348369.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202406667.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202429344.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202446673.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202506436.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181010205505966.png"></li>
              <li><img src="http://onlinegk.oss-cn-beijing.aliyuncs.com/upload/20181006202542822.png"></li>
              <li><img src="../../../assets/img/index/par/elven_icon.png"></li>
              <li><img src="../../../assets/img/index/par/twele_icon.png"></li>
          </ul>
        </div> -->
        <div class="shipei">
            <div class="center">
              <div class="wai">
                <h1>{{this.$t('public.home.along')}}</h1>
                <h6>{{this.$t('public.home.alongs')}}</h6>
                <div class="nei">
                  <ul>
                    <li class="one" @mouseover="overs" @mouseout="outs">
                        <!-- <img src="../../../assets/img/index/icon/home_icon_01.png" alt=""> -->
                        <!-- <img src="../../../assets/img/index/icon/home_icon_02.png" alt=""> -->
                        <div></div>
                        <span>App Store</span>
                         <p class="qr_code" v-if="shows">
                            <i>{{$t('main.sweep_downloads')}}</i>
                        </p>
                    </li>
                    <li @mouseover="over" @mouseout="out" class="two">
                        <!-- <img src="../../../assets/img/index/icon/home_icon_03.png" alt=""> -->
                        <!-- <img src="../../../assets/img/index/icon/home_icon_04.png" alt=""> -->
                        <div></div>
                        <span>Android</span>
                        <p class="qr_code" v-if="show">
                            <img src="../../../assets/img/index/下载.png" alt="">
                            <i>{{$t('main.sweep_download')}}</i>
                        </p>
                    </li>
                    <li class="three" @mouseover="overss" @mouseout="outss">
                        <!-- <img src="../../../assets/img/index/icon/home_icon_05.png" alt=""> -->
                        <!-- <img src="../../../assets/img/index/icon/home_icon_06.png" alt=""> -->
                        <div></div>
                        <span>Windows</span>
                         <p class="qr_code" v-if="showss">
                            <i>{{$t('main.sweep_downloads')}}</i>
                        </p>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
        </div>
      </div>
</template>
<script>
import echarts from 'echarts'
import { mapState } from 'vuex'
import pako from 'pako'
import slider from 'vue-concise-slider'
import BScroll from 'better-scroll'
export default {
  name: 'm-main',
  components: {    slider},
  computed: {
    ...mapState({
      public_info ({baseData}) {
        if (baseData.isReady && this.firstFlag) {
          this.baseData = baseData
          this.lang = baseData._lan
          this.creatWs()
          this.firstFlag = false
          return true
        } else {
          return true
        }
      }
    }),
    contentText () {
      return {
        nodeDataText: this.$t('main.loading_ing')
      }
    }
  },
  data () {
    return {
      flag: true,
      firstFlag: true,
      isArr: [], // 轮播图数据
      mack: 0,   // 图片索引
      time: null, // 定时器
      marketListWS: null,
      topMarket: null,
      symbolTop: {},
      skin: '',
      markTitle: localStorage.getItem('homeMarkTitle'),
      symbolListData: {},
      symbolListArr: [],
      symbolListArrs:[],
      lastSymbol: [],
      search: null,
      lang: localStorage.getItem('lan'),
      rate: '',
      baseData: {},
      aaa: '',
      frame: false,
      sortName: null,
      sortType: null,
      topMarketTrade: null,
      klineData: null,
      klineKey: null,
      myEcharts: {},
      theme: this.$store.state.baseData._theme,
      myMarket: localStorage.getItem('myMarket')
        ? localStorage.getItem('myMarket').split(',')
        : [],
      noticeInfoList: [],
      notice: null,  // 公告
      sildePage: [],
      isArr: [], // 轮播图数据
      mack: 0,   // 图片索引
      time: null, // 定时器
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
        thresholdDistance: 0,
        thresholdTime: 0,
        autoplay: false,
        loop: false,
        direction: 'horizontal',
        infinite: 1,
        slidesToScroll: 1,
        timingFunction: 'ease',
        duration: 0
      },
      show:false,
      shows:false,
      showss:false
    }
  },
  mounted () {
    this.getLundata()
  },
  destroyed () {
    if (this.marketListWS) {
      this.marketListWS.onclose()
    }
    if (this.topMarket) {
      this.topMarket.onclose()
    }
  },
  watch: {
    '$store.state.baseData._lan' (val, old) {
      // 重新请求轮播图
      if (old) {
        this.getLundata()
      }
    },
    // 监听货币对搜索
    search (val) {
      for (let i = 0; i < this.symbolListArr.length; i++) {
        this.symbolListArr[i].symbol.split('/')[0].indexOf(val.toUpperCase()) === -1
          ? (this.symbolListArr[i].isShow = false)
          : (this.symbolListArr[i].isShow = true)
      }
    },
    'symbolListData' (value) {
      let arr = []
      for (let item in value) {
        arr.push(value[item])
      }
      if (arr.length < 1) {
        this.contentText.nodeDataText = this.$t('main.no_data')
      }
      this.symbolListArr = arr
      this.symbolListArrs=this.symbolListArr.slice(0,5)
    },
    //  监听皮肤切换
    '$store.state.baseData._theme' (val, old) {
      if (!val) return false

      this.theme = val
      if (old) {
        // console.log(old)
        // this.initEachart(this.klineData, this.klineKey)
        for (let item in this.myEcharts) {
          console.log(item)
          this.myEcharts[item].setOption({
            series: {
              lineStyle: {
                normal: {
                  color: this.$store.state.color.HomeChartColor[this.theme].lineStyle,
                  width: 1
                }
              },
              areaStyle: {
                normal: {
                  color: this.$store.state.color.HomeChartColor[this.theme].areaStyle
                }
              }
            }
          })
        }
      }
    }
  },
  methods: {
    over () {
      this.show = true
    },
    out () {
      this.show = false
    },
    overs () {
      this.shows = true
    },
    outs () {
      this.shows = false
    },
    overss () {
      this.showss = true
    },
    outss () {
      this.showss = false
    },
    eachart (data, key) {
      this.myEcharts[key].resize()
      // console.log(this.myEcharts[key], data)
      this.myEcharts[key] && this.myEcharts[key].setOption({
        series: [
          {
            data: data
          }
        ]
      })
    },
    initEachart (data, key) {
      this.myEcharts[key] = echarts.init(document.getElementById('chart_' + key))
      // 绘制图表
      this.myEcharts[key] && this.myEcharts[key].setOption({
        grid: {
          left: 0,
          bottom: 0,
          top: 0,
          right: 0
        },
        xAxis: {
          show: false,
          type: 'category',
          min: 'dataMin',
          max: 'dataMax'
        },
        yAxis: {
          show: false,
          type: 'value',
          min: 'dataMin',
          max: 'dataMax'
        },
        series: [{
          data: data,
          type: 'line',
          symbol: 'none',
          // smooth: true,
          lineStyle: {
            normal: {
              color: this.$store.state.color.HomeChartColor[this.theme].lineStyle,
              width: 1
            }
          },
          areaStyle: {
            normal: {
              color: this.$store.state.color.HomeChartColor[this.theme].areaStyle
            }
          }
        }]
      })
    },
    // 市场切换
    tabTog (key) {
      if (key === 'myMarket') {
        if (this.baseData.isLogin) {
          this.getoptional()
        }
      }
      if (this.markTitle === key) {
        return
      }
      for (let i = 0; i < this.lastSymbol.length; i++) {
        this.sedWs(this.lastSymbol[i], 'unsub')
      }
      key !== 'myMarket' && localStorage.setItem('homeMarkTitle', key)
      this.markTitle = key
      this.markList()
    },

    creatWs () {
      // 创建ws
      this.marketListWS = new WebSocket(this.baseData._ws)
      this.marketListWS.binaryType = 'arraybuffer'
      this.topMarket = new WebSocket(this.baseData._ws)
      this.topMarket.binaryType = 'arraybuffer'
      // 建立连接
      this.marketListWS.onopen = evt => {
        this.markList()
      }
      // 获取数据
      this.marketListWS.onmessage = evt => {
        var na = new Uint8Array(evt.data)
        if (na.length > 0) {
          let data = JSON.parse(pako.inflate(na, { to: 'string' }))
          if (data['ping']) {
            this.marketListWS.send(JSON.stringify({ pong: data['ping'] }))
          } else if (data.tick) {
            let symbol = data.channel.split('_')[1]
            let symboList = this.baseData._symbols[this.markTitle]
            for (let v in symboList) {
              if (symboList[v].symbol === symbol) {
                this.addWsListData(symboList[v].name, data.tick)
              }
            }
          }
        }
      }
      this.marketListWS.onclose = evt => {
        console.log('关闭', evt)
      }
      this.marketListWS.onerror = evt => {
        console.log('错误', evt)
      }
      // 建立连接
      this.topMarket.onopen = ev => {
        this.symbolTopList()
      }
      // 获取数据
      this.topMarket.onmessage = evt => {
        var na = new Uint8Array(evt.data)
        if (na.length > 0) {
          let data = JSON.parse(pako.inflate(na, { to: 'string' }))
          if (data['ping']) {
            this.topMarket.send(JSON.stringify({ pong: data['ping'] }))
          } else if (data.event_rep && data.event_rep === 'rep' && data.data) { // 1分钟K线历史
            let key = data.channel.split('_')[1]
            if (!this.symbolTop[key]) return false
            this.myEcharts[key] = true
            if (data.data.length <= 0) return false
            this.symbolTop[key].kline = []
            for (let i = data.data.length - 1; i >= 0; i--) {
              if (i <= data.data.length - 100) break
              this.symbolTop[key].kline.push([data.data[i].id, data.data[i].close])
            }
            this.symbolTop[key].kline.reverse()
            this.initEachart(this.symbolTop[key].kline, key)
          } else if (data.tick && data.channel.indexOf('_kline_') > -1) { // 1分钟K线
            let key = data.channel.split('_')[1]
            if (this.symbolTop[key] && this.symbolTop[key].kline !== null && this.myEcharts[key]) {
              this.symbolTop[key].kline.length > 100 && this.symbolTop[key].kline.shift()
              this.symbolTop[key].kline.push([data.tick.id, data.tick.close])
              this.klineData = this.symbolTop[key].kline
              this.klineKey = key
              this.eachart(this.symbolTop[key].kline, key)
            }
          } else if (data.tick) { // 24小时行情
            let d = data.tick
            let key = data.channel.split('_')[1]
            let topMN = this.symbolTop[key].name.split('/')[1]  // 当前市场
            let j = this.baseData._symbols[topMN][this.symbolTop[key].name].price // 当前市场信息
            let oldClose = this.symbolTop[key].close.data // 上次价格
            let close = this._P.fixD(d.close, j)
            let rate = this._P.fixRate(d.close, this.baseData._rate, topMN)
            let Od = parseFloat(oldClose)
            let cs = parseFloat(close)
            let rs = ''
            if (Od + '' !== 'NaN') {
              cs > Od && (rs = 'c-fall')
              cs < Od && (rs = 'c-rise')
              cs === Od && (rs = '')
            }
            this.symbolTop[key].close = {
              class: rs,
              data: close + '/' + rate
            }
            let num = Math.abs(d.rose * 10000 / 100)
            let rose = null
            let rc = null
            if (isNaN(num)) {
              rose = '0.00%'
            } else {
              rose = Number(num.toString().match(/^\d+(?:\.\d{0,2})?/)) + '%'
              if (d.rose < 0) {
                rc = 'c-fall'
                rose = '-' + rose
              }
              if (d.rose > 0) {
                rc = 'c-rise'
                rose = '+' + rose
              }
              d.rose === 0 && (rc = '')
            }
            this.symbolTop[key].rose = {
              class: rc,
              data: rose
            }
            this.symbolTop[key].amount = this._P.fixD(d.amount, j)
            this.$forceUpdate()
          }
        }
      }
      this.topMarket.onclose = evt => {
        console.log('关闭', evt)
      }
      this.topMarket.onerror = evt => {
        console.log('错误', evt)
      }
    },
    symbolTopList () {
      for (let i = 0; i < this.$store.state.baseData._topSymbol.length; i++) {
        let s = this.$store.state.baseData._topSymbol[i]
        let sMarket = s.split('/')[1]
        let sWs = s.toLowerCase().split('/')
        let key = sWs[0] + sWs[1]
        this.symbolTop[key] = {
          close: {
            class: '',
            data: '--'
          },
          rose: {
            class: '',
            data: '--'
          },
          amount: '--',
          name: s,
          kline: null
        }
        this.$forceUpdate()
        if (this.$store.state.baseData._symbols[sMarket] && this.$store.state.baseData._symbols[sMarket][s]) {
          this.sendsymbolTop(key)
          this.myEcharts[key] = false
        }
      }
    },
    sendsymbolTop (symbol) {
      if (!this.topMarket) return
      this.topMarket.send(JSON.stringify({
        event: 'sub',
        params: {
          channel: 'market_' + symbol + '_ticker',
          cb_id: symbol
        }
      }))
      this.topMarket.send(JSON.stringify({
        event: 'req',
        params: {
          channel: 'market_' + symbol + '_kline_1min',
          cb_id: symbol
        }
      }))
      this.topMarket.send(JSON.stringify({
        event: 'sub',
        params: {
          channel: 'market_' + symbol + '_kline_1min',
          cb_id: symbol
        }
      }))
    },
    markList () {
      !this.markTitle && (this.markTitle = this.baseData._maket_index)
      let sList = this.baseData._symbols[this.markTitle]
      this.symbolListData = {}
      this.lastSymbol = []
      for (let item in sList) {
        let unit = sList[item].name.split('/')[1]
        if (this.baseData._symbols[unit][item]) {
          this.symbolListData[sList[item].name] = {
            isShow: true,
            close: {
              class: '',
              data: '--'
            },
            rose: {
              class: '',
              data: '--'
            },
            high: '--',
            low: '--',
            vol: '--',
            amount: '--'
          }
          this.lastSymbol.push(sList[item].symbol)
          this.sedWs(sList[item].symbol, 'sub')
        }
      }
    },
    sedWs (symbol, type) {
      this.marketListWS.send(JSON.stringify({
        event: type,
        params: {
          channel: 'market_' + symbol + '_ticker',
          cb_id: symbol
        }
      }))
    },
    addWsListData (name, data) {
      let t = this.symbolListData[name]
      let thisMarket = this.baseData._symbols[name.split('/')[1]]
      // 最新价
      let oldClose = t.close.data
      let close = this._P.fixD(data.close, thisMarket[name].price)
      let rate = this._P.fixRate(data.close, this.baseData._rate, name.split('/')[1].toUpperCase())
      let Od = parseFloat(oldClose)
      let cs = parseFloat(close)
      let rs = ''
      if (Od + '' !== 'NaN') {
        cs > Od && (rs = 'c-fall')
        cs < Od && (rs = 'c-rise')
        cs === Od && (rs = '')
      }
      t.close = {
        class: rs,
        data: close + '/' + rate
      }
      let symbolname = name.split('/')[0]
      let coin = name.split('/')[1]
      t.symbolname = symbolname
      t.coin = coin
      t.symbol = symbolname + '/' + coin
      // 涨跌

      let num = Math.abs(data.rose * 10000 / 100)
      let rose = null
      let rc = null
      if (isNaN(num)) {
        rose = '0.00%'
      } else {
        rose = Number(num.toString().match(/^\d+(?:\.\d{0,2})?/)) + '%'
        if (data.rose < 0) {
          rc = 'c-fall'
          rose = '-' + rose
        }
        if (data.rose > 0) {
          rc = 'c-rise'
          rose = '+' + rose
        }
        if (data.rose === 0) {
          rc = ''
          rose = '0.00%'
        }
      }
      t.rose = {
        class: rc,
        data: rose
      }
      t.high = this._P.fixD(data.high, thisMarket[name].price)
      t.low = this._P.fixD(data.low, thisMarket[name].price)
      t.vol = this._P.fixD(data.vol, thisMarket[name].volume)
      t.amount = this._P.fixD(data.amount, thisMarket[name].price)
      // this.aaa = this._P.fixD(data.amount, thisMarket[name].price)
      this.$forceUpdate()
    },
    changeMysymbol (symbol) {
      if (this.myMarket.indexOf(symbol) > -1) {
        this.myMarket = this.myMarket.filter(function (item, index, array) {
          return item !== symbol
        })
      } else {
        this.myMarket.push(symbol)
      }
      localStorage.setItem('myMarket', this.myMarket)
      let newMyMarket = {}
      for (let i = 0; i < this.myMarket.length; i++) {
        let tempSymbol = this.myMarket[i].split('/')
        newMyMarket[this.myMarket[i]] = {
          'name': this.myMarket[i],
          'symbol': tempSymbol[0].toLowerCase() + tempSymbol[1].toLowerCase()
        }
      }
      this.$store.commit('MYMARKET', newMyMarket)
      if (this.baseData.isLogin) {
        this.getoptional()
      }
      if (this.markTitle === 'myMarket') {
        for (let i = 0; i < this.symbolListArr.length; i++) {
          if (this.symbolListArr[i].symbol === symbol) {
            this.symbolListArr.splice(i, 1)
          }
        }
      }
    },
    getoptional () {
      this.axios({
        url: this.$store.state.url.common.optional_symbol,
        headers: {},
        params: {
          optional_symbol: this.myMarket,
          time: new Date().getTime()
        },
        method: 'post'
      }).then((data) => {
        if (data.code === '0') {
        } else {
          this.$store.dispatch('setTipState', {text: data.msg, type: 'error'})
        }
      })
    },
    issue () {
      this.frame = true
    },
    lose () {
      this.frame = false
    },
    marketSor (val) {
      if (val !== this.sortName || this.sortType === 'ups') {
        this.symbolListArr = this.quickSort(this.symbolListArr, val).reverse()
        this.sortName = val
        this.sortType = 'dow'
      } else {
        this.symbolListArr = this.quickSort(this.symbolListArr, val)
        this.sortType = 'ups'
      }
    },
    marketSort (val) {
      if (val !== this.sortName || this.sortType === 'up') {
        this.symbolListArr = this.quickSort(this.symbolListArr, val).reverse()
        this.sortName = val
        this.sortType = 'down'
      } else {
        this.symbolListArr = this.quickSort(this.symbolListArr, val)
        this.sortType = 'up'
      }
    },
    quickSort (dataArrer, key) {
      if (dataArrer.length <= 1) {
        return dataArrer
      }
      let index = Math.floor(dataArrer.length / 2)
      let temp = dataArrer.splice(index, 1)
      let leftArr = []
      let rightArr = []
      for (let i = 0; i < dataArrer.length; i++) {
        if (parseFloat(dataArrer[i][key]['data']) < parseFloat(temp[0][key]['data']) || dataArrer[i][key]['data'] === '--') {
          leftArr.push(dataArrer[i])
        } else {
          rightArr.push(dataArrer[i])
        }
      }
      return this.quickSort(leftArr, key).concat(temp, this.quickSort(rightArr, key))
    },
    transaction (item) {
      localStorage.setItem('sSymbolName', item)
      localStorage.setItem('markTitle', this.markTitle)
      this.$router.push({ name: 'coinTran' })
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
            this.noticeInfoList=this.noticeInfoList.slice(0,5)
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
<style>
.symboy_bgc:hover{
  background:#F4F5F9;
}
.advantage{ 
  width: 100%;
  margin: 0 auto;
  padding:150px 0 0 0; 
  background: #f8f8f8; 
  overflow: hidden;
}
.advantage ul{
  width: 90%;
  margin: 0 auto;
}
.advantage ul li{
  display:block; 
  float: left; 
  width: 33.3%; 
}
.advantage ul li span{
  display:block; 
  padding: 0px 0px 0px 0px; 
  text-align: center;
  }
.advantage ul li p{
  display:block; 
  padding:20px; 
  margin: 0px; 
  text-align: center; 
  font-size: 18px; 
  line-height: 54px; 
  color:#000;
  font-weight: 540;
  }
.advantage ul li i{
  display:block; 
  padding:0px 30px 40px 30px; 
  line-height:30px; 
  text-align: center;
  font-style:normal; 
  font-size: 12px; 
  color: #DEDEDE;
  }
.cooperation{ 
  padding:50px 20px; 
  background:#f8f8f8; 
  overflow: hidden;
  text-align: center;
  }
.cooperation p{
  display:block; 
  margin: 0px; 
  padding: 20px 0px; 
  font-size: 38px; 
  text-align: center; 
  line-height:60px; 
  color:#000;
  }
.cooperation font{
    color: #898989;
    font-size: 20px;
  }
.cooperation ul{
  min-width: 1800px; 
  margin: 50px auto; 
  max-width:1800px;
  margin-left: 8%;
  }
.cooperation ul li{
   width: 214px; 
   height: 100px; 
   background: #EEEEEE;
   float: left; 
   margin: 10px 30px 30px 20px;
   }
.shipei{
  width: 100%;
  height: 410px;
  overflow: hidden;
  background: #fff;
  }
.shipei .center{
    width: 85%;
    min-width: 1200px;
    margin: 0 auto;
}
.shipei .center .wai{
  width: 1000px;
  height:1000px;
  margin: 0 auto;
  background: #fff;
  border-radius: 50%;
  border:75px solid #F6F7FB;
  text-align: center;
}
.shipei .center .wai h1{
  font-size: 32px;
  color: #000;
}
.shipei .center .wai h6{
  font-size: 14px;
  color: #B0B0B0;
  line-height: 42px;
}
.shipei .center .wai .nei{
  width:700px;
  height:700px;
  margin: 20px auto;
  background: #fff;
  border-radius: 50%;
  border:75px solid #F6F7FB;
}
.shipei .center .wai .nei ul{
  width: 80%;
  height: 50px;
  display: flex;
  margin: 0 auto;
}
.shipei .center .wai .nei ul li{
  width: 30%;
  height: 46px;
  color: #333;
  border:2px solid #333;
  border-radius: 23px;
  display: flex;
  align-items: center;
  margin-left: 30px;
  cursor: pointer;
  background: #fff;
}
.shipei .center .wai .nei ul li div{
  width: 24px;
  height: 24px;
  margin-left: 30px;
}
.shipei .center .wai .nei ul li span{
  margin-left: 10px;
}
.shipei .center .wai .nei ul .one div{
  background-image: url("../../../assets/img/index/icon/home_icon_02.png")
}
.shipei .center .wai .nei ul .one:hover div{
  background-image: url("../../../assets/img/index/icon/home_icon_01.png")
}
.shipei .center .wai .nei ul .two div{
  background-image: url("../../../assets/img/index/icon/home_icon_04.png")
}
.shipei .center .wai .nei ul .two:hover div{
  background-image: url("../../../assets/img/index/icon/home_icon_03.png")
}
.shipei .center .wai .nei ul .three div{
  background-image: url("../../../assets/img/index/icon/home_icon_06.png")
}
.shipei .center .wai .nei ul .three:hover div{
  background-image: url("../../../assets/img/index/icon/home_icon_05.png")
}
.shipei .center .wai .nei ul li:hover{
  color: #3076f6;
  border: 2px solid #3076f6;
}
.shipei .center .wai .nei ul .one,.two,.three{
  position: relative;
}
.shipei .center .wai .nei ul .one,.three .qr_code i{
  line-height: 100px;
}
.qr_code{
  width:100px;
  height:115px;
  background:#fff;
  position:absolute;
  top: 50px;
  left: 20%;
  border-radius:4px;
}
.qr_code img{
  width: 100px;
  height: 100px;
}
</style>






