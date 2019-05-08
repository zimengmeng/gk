<template>
  <div style="overflow: hidden; background: #080218;">
    <Header></Header>
    <p v-if="!public_info"></p>
    <div class="window_mine" v-show="mining_rules">
      <div class="imgclose" style="margin:20px 0px 0px 555px;" @click="mining_rules=false">
        <img src="../../assets/img/mineimg/img_close.png">
      </div>
      <div class="window_mine_content">
        <dl>
          <dt style="padding-bottom: 20px;">{{$t('mining.mnrules')}}</dt>
          <dd>{{$t('mining.mnrulesone')}}</dd>
          <dd>{{$t('mining.mnrulestwo')}}</dd>
          <dd>{{$t('mining.mnrulesthree')}}</dd>
          <dd>{{$t('mining.mnrulesfour')}}</dd>
          <dd>{{$t('mining.mnrulesfive')}}</dd>
          <dd>{{$t('mining.mnrulessix')}}</dd>
          <dd>{{$t('mining.mnrulesseven')}}</dd>
          <dd style="padding-top: 20px; color: #b8b8b8;line-height: 24px;">{{$t('mining.mnrulesgk')}}
            <br>{{$t('mining.mnrulesthanks')}}</dd>
        </dl>
      </div>
    </div>
    <div class="window_bg" v-show="mining_rules"></div>

    <div class="gko">
      <a href="#gko">
        <img src="../../assets/img/mineimg/img_gkc.png">
      </a>
    </div>

    <div class="banner_bg">
      <div class="banner">
        <div class="banner_top fn_white">
          <span>{{$t('mining.mnrulesadtop')}}</span>
        </div>
        <div class="banner_content fn_white">
          <span>{{$t('mining.mnrulesadleft')}}</span>
          <i>
            <img src="../../assets/img/mineimg/img_number.png">
          </i>
          <span>{{$t('mining.mnrulesadright')}}</span>
        </div>
        <div class="banner_foot">
          {{$t('mining.mnrulesadbottom')}}
          <br>{{$t('mining.mnrulesadbottomtwo')}}
        </div>
        <div class="banner_button">
          <a href="https://www.gk.com/trade">
            <span class="bb fng_button">{{$t('mining.mnrulesexchange')}}</span>
          </a>
        </div>
      </div>
    </div>
    <div class="common_box">
      <div class="common_box_top">
        <!-- <ul>
          <li>
            <div :class="{teb_yellow: gk3Time[0], teb_black: !gk3Time[0]}">
              <p v-if="gk3Time[0]">{{$t('mining.stagenoe01')}}</p>
              <p v-if="!gk3Time[0]">{{$t('mining.stagenoe02')}}</p>
              <span>{{$t('mining.stagenoe03')}}</span>
            </div>
            <div v-if="gk3Time[0]" class="teb_bg"></div>
          </li>
          <li>
            <div :class="{teb_yellow: gk3Time[1], teb_black: !gk3Time[1]}" style="border-right: 1px solid #221130;">
              <p v-if="gk3Time[1]">{{$t('mining.stagetwo01')}}</p>
              <p v-if="!gk3Time[1]">{{$t('mining.stagetwo02')}}</p>
              <span>{{$t('mining.stagetwo03')}}</span>
            </div>
            <div v-if="gk3Time[1]" class="teb_bg"></div>
          </li>
          <li style="width: 34%;">
            <div :class="{teb_yellow: gk3Time[2], teb_black: !gk3Time[2]}">
              <p v-if="gk3Time[2]">{{$t('mining.stagethree01')}}</p>
              <p v-if="!gk3Time[2]">{{$t('mining.stagethree02')}}</p>
              <span>{{$t('mining.stagethree03')}}</span>
            </div>
            <div v-if="gk3Time[2]" class="teb_bg"></div>
          </li>
        </ul> -->
        <ul>
          <li>
            <div class="teb_yellow">
              <p v-if="isShow">{{$t('mining.stagenoe01')}}</p>
              <p v-if="!isShow">{{$t('mining.stagenoe02')}}</p>
              <span>{{$t('mining.stagenoe03')}}</span>
            </div>
            <div v-if="isShow" class="teb_bg"></div>
          </li>
          <li>
            <div class="teb_black" style="border-right: 1px solid #221130;">
              <p v-if="isShow">{{$t('mining.stagetwo01')}}</p>
              <p v-if="!isShow">{{$t('mining.stagetwo02')}}</p>
              <span>{{$t('mining.stagetwo03')}}</span>
            </div>
            <div v-if="!isShow" class="teb_bg"></div>
          </li>
          <li style="width: 34%;">
            <div class="teb_black">
              <p v-if="isShow">{{$t('mining.stagethree01')}}</p>
              <p v-if="!isShow">{{$t('mining.stagethree02')}}</p>
              <span>{{$t('mining.stagethree03')}}</span>
            </div>
            <div v-if="!isShow" class="teb_bg"></div>
          </li>
        </ul>
      </div>
      <div v-if="isShow">
        <div class="mining_in">
          <span style="display: block;position: absolute; z-index: 5; width: 300px; height: 40px; line-height: 40px; color: #fff; text-align: center; left: 50%; margin-left: -150px;font-size: 14px;">
            {{$t('mining.mnschedule')}}{{((inviData.total_return_number / 64000000) * 100).toFixed(2)}}%
          </span>
          <div class="schedule">
            <div class="container">
              <div class="warning" style="min-width:10px" :style="{width: ((inviData.total_return_number / 64000000) * 100).toFixed(2) + '%'}"></div>
            </div>
          </div>
        </div>
        <div class="default_text">
          <span>0 GKO</span>
          <i>64000000 GKO</i>
        </div>
        <div class="count">
          <ul>
            <li>
              <div style="padding-right: 20px;">
                <div class="count_bg">
                  <p v-if="inviData.today_return_number">{{inviData.today_return_number + ' ' + inviData.coin}}</p>
                  <p v-else>{{0+ '.GKO'}}</p>
                  <span>{{$t('mining.distribution')}}</span>
                </div>
              </div>
            </li>
            <li style="width: 34%;">
              <div style="padding: 0px 20px;">
                <div class="count_bg">
                  <p v-if="inviData.yesterday_return_number">{{inviData.yesterday_return_number + ' ' + inviData.coin}}</p>
                  <p v-else>{{0+ '.GKO'}}</p>
                  <span>{{$t('mining.mining_output')}}</span>
                </div>
              </div>
            </li>
            <li>
              <div style="padding-left: 20px;">
                <div class="count_bg">
                  <p v-if="inviData.total_return_number">{{inviData.total_return_number + ' ' + inviData.coin}}</p>
                  <p v-else>{{0+ '.GKO'}}</p>
                  <span>{{$t('mining.mntotaldiggers')}}</span>
                </div>
              </div>
            </li>
          </ul>
        </div>
        <div class="countlink fn_white">
          <a @click="mining_rules=true">{{$t('mining.mnlookrule')}}</a>
        </div>
      </div>
      <div v-else>
        <div class="minesurplus" v-if="inviData.total_return_number > 0 && inviData.total_return_number < 64000000">
          {{$t('mining.mncompleted')}}
        </div>
        <div class="minesurplus" v-if="inviData.total_return_number >= 64000000">
          {{$t('mining.mnnocompleted')}}
        </div>
      </div>
    </div>
    <div class="about" id="gko">
      <div class="about_token">
        <p>
          <img src="../../assets/img/mineimg/img_mine.png">
        </p>
        <span>GKO</span>
        <i>{{$t('mining.gkointroduceneo')}}
          <br>{{$t('mining.gkointroducetwo')}}
        </i>
      </div>
      <div class="about_token">
        <p>
          <img src="../../assets/img/mineimg/img_token.png">
        </p>
        <span>{{$t('mining.gkexchange')}}</span>
        <i>{{$t('mining.gkexchangeone')}}
          <br>{{$t('mining.gkexchangetwo')}}
          <br>{{$t('mining.gkexchangethree')}}</i>
      </div>
    </div>
    <Footer></Footer>
  </div>
</template>
<script>
  import { mapState } from "vuex";
  import Header from '../module/header.vue'
  import Footer from '../module/footer.vue'
  export default {
    name: "m-main",
    components: {Header,Footer},
    data() {
      return {
        firstFlag: true,
        sildePage: [],
        isArr: [], // 轮播图数据
        mack: 0, // 图片索引
        time: null, // 定时器
        notice: null, // 公告
        isShow: true,//显示隐藏
        sliderinit: {
          currentPage: 0,
          thresholdDistance: 500,
          thresholdTime: 100,
          autoplay: 10000,
          loop: true,
          infinite: 1,
          slidesToScroll: 1,
          timingFunction: "ease",
          duration: 300
        },
        inviData: {
          total_return_number: 0
        },
        itemArray: [],
        tabTitle: "mining",
        inviDatas: {
          count: 0,
          page: 1,
          display: 10
        },
        dividend: {
          count: 0,
          page: 1,
          display: 10
        },
        dividends: {
          count: 0,
          page: 1,
          display: 10
        },

        baseData: "",
        loading_entrust: false,
        gk3Time: [],
        mining_rules: false,
        inviting_rules: false
      };
    },
    created() {
      setTimeout(function head() {
        var mh = document.querySelectorAll('.m-header')[0];
        if (!mh) {
          setTimeout(head, 20);
        } else {
          mh.className = 'm-header gk_hdtop'
        }
      }, 20);
    },
    beforeDestroy() {
      setTimeout(function head() {
        var mh = document.querySelectorAll('.m-header')[0];
        if (!mh) {
          setTimeout(head, 20);
        } else {
          mh.className = 'm-header'
        }
      }, 20);
    },
    mounted() {
      this.getLundata();
    },
    computed: {
      ...mapState({
        public_info({ baseData }) {
          if (baseData.isReady && this.firstFlag) {
            this.baseData = baseData;
            this.getInvition();
            this.firstFlag = false;
            return baseData;
          } else {
            return true;
          }
        }
      }),
      minin() {
        return [this.$t("mining.replaced"), this.$t("mining.Return")];
      }
    },
    watch: {
      // 监听 语言切换
      "$store.state.baseData._lan"(val, old) {
        // 重新请求轮播图
        if (old) {
          this.getLundata();
        }
      }
    },
    methods: {
      getLundata() {
        this.axios({
          url: this.$store.state.url.common.index_data,
          headers: {},
          params: {},
          method: "post"
        }).then(data => {
          if (data.code === "0") {
            this.notice = data.data.noticeInfo;
            let res = data.data.cmsAdvertList;
            this.isArr = [];
            let arr = [];
            for (let i = 0; i < res.length; i++) {
              let obj = {};
              obj.html = '<div><img src="' + res[i].imageUrl + '"></div>';
              arr.push(obj);
              this.isArr.push(res[i]);
            }
            this.sildePage = arr;
          } else {
            this.$store.dispatch("setTipState", {
              text: data.msg,
              type: "error"
            });
          }
        });
      },
      tabTog(i) {
        this.tabTitle = i;
        // this.getInvition()
      },
      onTap(data) {
        window.open(this.isArr[data.currentPage].httpUrl);
      },
      getInvition() {
        this.axios({
          url: this.$store.state.url.return.mining,
          headers: {},
          params: {
            page:
              this.inviDatas.page || this.dividend.page || this.dividends.page,
            pageSize: 10
          },
          method: "post"
        }).then(data => {
          var dtime = +new Date(data.gkServerDateTime);
          this.gk3Time = [
            dtime < +new Date(2018, 11, 1),
            dtime > +new Date(2018, 11, 1) && dtime < +new Date(2019, 0, 1),
            dtime > +new Date(2019, 0, 1) && dtime < +new Date(2019, 1, 1)
          ];
          if (data.code === "0") {
            this.loading_entrust = false;
            let mindata = data.data;
            // console.log(mindata);
            mindata.total_return_number = this._P.fixD(
              mindata.total_return_number,
              this.baseData._coinList[mindata.coin].showPrecision
            );
            mindata.today_return_number = this._P.fixD(
              mindata.today_return_number,
              this.baseData._coinList[mindata.coin].showPrecision
            );
            mindata.today_dividend_number = this._P.fixD(
              mindata.today_dividend_number,
              this.baseData._coinList[mindata.coin].showPrecision
            );
            mindata.yesterday_return_number = this._P.fixD(
              mindata.yesterday_return_number,
              this.baseData._coinList[mindata.coin].showPrecision
            );
            mindata.yesterday_dividend_number = this._P.fixD(
              mindata.yesterday_dividend_number,
              this.baseData._coinList[mindata.coin].showPrecision
            );
            for (let i in mindata.return_list) {
              mindata.return_list[i].return_number_btc = this._P.fixD(
                mindata.return_list[i].return_number_btc,
                this.baseData._coinList["BTC"].showPrecision
              );
              mindata.return_list[i].return_number = this._P.fixD(
                mindata.return_list[i].return_number,
                this.baseData._coinList[mindata.coin].showPrecision
              );
              mindata.return_list[i].dtime = this._P.formatTime(
                mindata.return_list[i].dtime
              );
            }
            for (let iten in mindata.dividend_list) {
              mindata.dividend_list[iten].fee = this._P.fixD(
                mindata.dividend_list[iten].fee,
                this.baseData._coinList[mindata.dividend_list[iten].coin]
                  .showPrecision
              );
              mindata.dividend_list[iten].dividend_number = this._P.fixD(
                mindata.dividend_list[iten].dividend_number,
                this.baseData._coinList[mindata.dividend_list[iten].coin]
                  .showPrecision
              );
            }
            for (let iten in mindata.yesterday_dividend_list) {
              mindata.yesterday_dividend_list[iten].fee = this._P.fixD(
                mindata.yesterday_dividend_list[iten].fee,
                this.baseData._coinList[
                  mindata.yesterday_dividend_list[iten].coin
                ].showPrecision
              );
              mindata.yesterday_dividend_list[
                iten
              ].dividend_number = this._P.fixD(
                mindata.yesterday_dividend_list[iten].dividend_number,
                this.baseData._coinList[
                  mindata.yesterday_dividend_list[iten].coin
                ].showPrecision
              );
            }
            this.inviDatas.count = mindata.return_count;
            this.inviData = mindata;
            this.$forceUpdate();
          } else {
            this.$store.dispatch("setTipState", {
              text: data.msg,
              type: "error"
            });
          }
        });
      },
      inviDatapage(i) {
        this.inviDatas.page = i;
        this.getInvition();
        this.loading_entrust = true;
      },
      dividendpage(i) {
        this.dividend.page = i;
        this.getInvition();
        this.loading_entrust = true;
      },
      dividendsp(i) {
        this.loading_entrust = true;
        this.getInvition();
        this.dividends.page = i;
      }
    }
  };
</script>

<style scoped>
  .fn_white,
  .fn_white a:link,
  .fn_white a:visited {
    color: #fff;
    text-decoration: none;
  }

  .fn_white a:hover {
    color: #0066ff;
  }

  .banner_bg {
    width: 100%;
    height: 800px;
    background: url(../../assets/img/mineimg/img_hd_bg.png) center bottom no-repeat;
  }

  .banner {
    overflow: hidden;
    height: 400px;
    padding: 150px 0px;
  }

  .banner_top {
    width: 100%;
    text-align: center;
    height: 100px;
    line-height: 100px;
  }

  .banner_top span {
    font-size: 24px;
  }

  .banner_top i {
    font-style: normal;
    font-size: 14px;
    padding: 0px 20px;
  }

  .banner_content {
    width: 764px;
    margin: 0px auto;
    height: 120px;
    overflow: hidden;
  }

  .banner_content span {
    display: block;
    float: left;
    width: 100px;
    font-size: 18px;
    text-align: center;
    line-height: 120px;
  }

  .banner_content i {
    display: block;
    float: left;
  }

  .banner_foot {
    width: 100%;
    padding-top: 30px;
    overflow: hidden;
    text-align: center;
    font-size: 14px;
    color: #666;
    line-height: 30px;
  }

  .banner_button {
    width: 160px;
    height: 50px;
    padding: 25px 0px;
    margin: 0px auto;
    font-size: 14px;
  }

  .banner_button span {
    display: block;
    width: 160px;
    height: 50px;
    line-height: 50px;
    float: left;
    margin: 0px 20px;
  }

  .bb {
    background: #ffca10;
    text-align: center;
    border-radius: 30px;
  }

  .bb:hover {
    background: #0d5dff;
    color: #fff;
  }

  .invitation {
    border: 2px solid #462f5a;
    background: #260a40;
    border-radius: 30px;
    text-align: center;
  }

  .invitation:hover {
    border: 2px solid #fff;
  }

  .fnw_button,
  .fnw_button a:link,
  .fnw_button a:visited {
    color: #fff;
    text-decoration: none;
  }

  .fnw_button a:hover {
    color: #fff;
  }

  .fng_button,
  .fng_button a:link,
  .fng_button a:visited {
    color: #333;
    text-decoration: none;
  }

  .fng_button a:hover {
    color: #333;
  }

  .common_box {
    width: 85%;
    min-width: 1200px;
    background: #160425;
    z-index: 2;
    margin: -100px auto 0px auto;
  }

  .common_box_top {
    width: 100%;
    height: 110px;
    overflow: hidden;
  }

  .common_box_top ul li {
    display: block;
    float: left;
    width: 33%;
    height: 110px;
    cursor: pointer;
  }

  .teb_yellow {
    width: 100%;
    height: 100px;
    background: #ffca10;
  }

  .teb_yellow p {
    display: block;
    padding: 0px;
    margin: 0px;
    text-align: center;
    width: 100%;
    font-size: 20px;
    line-height: 60px;
    color: #333;
  }

  .teb_yellow span {
    display: block;
    text-align: center;
    width: 100%;
    font-size: 14px;
    color: #ad890a;
  }

  .teb_bg {
    width: 100%;
    height: 10px;
    overflow: hidden;
    background: url(../../assets/img/mineimg/img_tebbg.png) no-repeat center bottom;
  }

  .teb_black {
    width: 100%;
    height: 100px;
    border-bottom: 1px solid #221130;
  }

  .teb_black p {
    display: block;
    padding: 0px;
    margin: 0px;
    text-align: center;
    width: 100%;
    font-size: 20px;
    line-height: 60px;
    color: #666;
  }

  .teb_black span {
    display: block;
    text-align: center;
    width: 100%;
    font-size: 14px;
    color: #666;
  }

  .mining_in {
    padding: 60px 60px 0px 60px;
    overflow: hidden;
  }

  .schedule {
    width: 100%;
    height: 40px;
    background: #11021d;
    border: 1px solid #221130;
  }

  .default_text {
    padding: 0px 60px 0px 60px;
    overflow: hidden;
    line-height: 40px;
    color: #666;
    font-size: 14px;
  }

  .default_text span {
    display: block;
    float: left;
  }

  .default_text i {
    display: block;
    float: right;
    font-style: normal;
  }

  .count {
    overflow: hidden;
    padding: 40px 60px 0px 60px;
  }

  .count ul li {
    float: left;
    width: 33%;
    overflow: hidden;
  }

  .count_bg {
    height: 100px;
    padding: 25px 0px;
    background: #11021d;
  }

  .count_bg p {
    display: block;
    margin: 0px;
    padding: 0px;
    overflow: hidden;
    width: 100%;
    line-height: 60px;
    color: #fff;
    font-size: 24px;
    text-align: center;
  }

  .count_bg span {
    display: block;
    width: 100%;
    text-align: center;
    line-height: 40px;
    color: #666;
    font-size: 14px;
  }

  .countlink {
    width: 100%;
    overflow: hidden;
    text-align: center;
    padding: 60px 0px;
    font-size: 14px;
  }

  .invite_list {
    overflow: hidden;
  }

  .invite_list dl dt {
    width: 100%;
    overflow: hidden;
    padding-top: 20px;
  }

  .invite_list dl dt span {
    float: left;
    text-align: center;
    line-height: 50px;
    color: #666;
    font: 14px;
    display: block;
    line-height: 50px;
  }

  .invite_list dl dd {
    width: 100%;
    overflow: hidden;
    cursor: pointer;
  }

  .invite_list dl dd span {
    float: left;
    text-align: center;
    line-height: 80px;
    color: #fff;
    font: 14px;
    display: block;
    line-height: 80px;
  }

  .invite_list dl dd:hover {
    background: #11021d;
  }

  .about {
    width: 85%;
    min-width: 1200px;
    overflow: hidden;
    padding: 80px 0px;
    background: #160425;
    z-index: 2;
    margin: 60px auto 0px auto;
    margin-bottom: 60px;
  }

  .about_token {
    width: 50%;
    overflow: hidden;
    float: left;
  }

  .about_token p {
    display: block;
    margin: 0px;
    padding: 0px;
    text-align: center;
  }

  .about_token span {
    display: block;
    overflow: hidden;
    text-align: center;
    font-size: 30px;
    color: #fff;
  }

  .about_token i {
    font-style: normal;
    display: block;
    overflow: hidden;
    padding: 20px 80px;
    line-height: 30px;
    color: #666;
    text-align: center;
    font-size: 14px;
  }

  .gko {
    width: 60px;
    height: 80px;
    overflow: hidden;
    position: fixed;
    z-index: 2;
    right: 0px;
    top: 400px;
    cursor: pointer;
  }

  .window_bg {
    width: 100%;
    height: 120%;
    background: #000;
    position: fixed;
    z-index: 88;
    opacity: 0.75;
    top: -100px;
  }

  .window_invite {
    width: 560px;
    padding: 20px;
    overflow: hidden;
    background: #ffca10;
    border-radius: 8px;
    position: fixed;
    z-index: 99;
    top: 50%;
    left: 50%;
    margin: -365px 0px 0px -300px;
  }

  .window_invite_content {
    width: 560px;
    height: 730px;
    background: #fff;
  }

  .window_invite_content dl {
    padding: 40px 30px 0px 30px;
  }

  .window_invite_content dl dt {
    display: block;
    width: 100%;
    font-size: 14px;
    line-height: 40px;
  }

  .window_invite_content dl dt span {
    color: #333;
  }

  .window_invite_content dl dt em {
    color: #b8b8b8;
    font-style: normal;
  }

  .window_invite_content dl dd {
    color: #333;
    font-size: 14px;
  }

  .window_invite_content dl dd a,
  .window_invite_content dl dd a:visited {
    margin-left: 20px;
    text-decoration: none;
  }

  .window_invite_content dl dd a:hover {
    margin-left: 20px;
    text-decoration: none;
    color: #8e7cff;
  }

  .window_invite_content dl dd p {
    color: #b8b8b8;
    line-height: 30px;
  }

  .imgclose {
    width: 20px;
    height: 20px;
    overflow: hidden;
    position: absolute;
    z-index: 100;
    margin: 20px 0px 0px 515px;
    cursor: pointer;
  }

  .window_mine {
    width: 600px;
    padding: 20px;
    overflow: hidden;
    background: #ffca10;
    border-radius: 8px;
    position: fixed;
    z-index: 99;
    top: 150px;
    left: 50%;
    margin: 0px 0px 0px -320px;
  }

  .window_mine_content {
    width: 600px;
    overflow: hidden;
    background: #fff;
    color: #333;
  }

  .window_mine_content dl {
    padding: 20px;
    font-size: 12px;
  }

  .window_mine_content dl dd {
    line-height: 30px;
  }

  .warning {
    position: relative;
    background-color: #1a65ff;
    background-size: 3em 3em;
    background-image: linear-gradient( -45deg,
    transparent 0em,
    transparent 0.8em,
    #0054ff 0.9em,
    #0054ff 2.1em,
    transparent 2.1em,
    transparent 2.9em,
    #0054ff 3.1em);
    -webkit-animation: warning-animation 750ms infinite linear;
    -moz-animation: warning-animation 750ms infinite linear;
    animation: warning-animation 750ms infinite linear;
  }

  @-webkit-keyframes warning-animation {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 3em 0;
    }
  }

  @-moz-keyframes warning-animation {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 3em 0;
    }
  }

  @keyframes warning-animation {
    0% {
      background-position: 0 0;
    }
    100% {
      background-position: 3em 0;
    }
  }

  .warning:before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    height: 40px;
  }

  .container {
    margin: 0;
    background: #11021d;
  }

  .container .warning {
    height: 10vh;
  }

  .minesurplus {
    width: 100%;
    overflow: hidden;
    text-align: center;
    padding: 60px 0px;
    font-size: 14px;
    color: #fff;
  }
</style>