<template>
   <div>
        <Header class="header"></Header>
        <div class="grade">
            <div class="grade_banner">
            <div class="subheading"><i>{{this.$t('public.home.blockchain')}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{{this.$t('public.home.sunshine')}}</i></div>
            <div class="maintitle"><i>{{this.$t('public.home.number')}}</i></div>
            <div class="describe"><i>Two-way Rating of Digital Assets</i></div>
            </div>	
            <div class="grade_introduce">
                {{this.$t('public.home.introduce')}}
            </div>
            <div class="grade_project">
                <p>{{this.$t('public.home.standard')}}</p>
                <ul>
                    <li>
                        <div class="grade_icon"><img src="../../../assets/img/dubble/icon_grade_01.png"></div>
                        <div class="grade_text">
                            <!--  -->
                            <h2>{{this.$t('public.home.score')}}</h2>
                            <span><i>{{this.$t('public.home.team')}}</i><i>{{this.$t('public.home.business')}}</i><i>{{this.$t('public.home.operation')}}</i><i>{{this.$t('public.home.market')}}</i><i>{{this.$t('public.home.feng')}}</i><i>{{this.$t('public.home.deng')}}</i></span>
                        </div>
                    </li>
                    <li>
                        <div class="grade_icon"><img src="../../../assets/img/dubble/icon_grade_02.png"></div>
                        <div class="grade_text">
                            <h2>{{this.$t('public.home.dongtai')}}</h2>
                            <span><i>{{this.$t('public.home.circulational')}}</i><i>{{this.$t('public.home.mobility')}}</i><i>{{this.$t('public.home.rate')}}</i><i>{{this.$t('public.home.volume')}}</i></span>
                        </div>
                        <div class="grade_time">
                            <div class="grade_time_in">
                                <img src="../../../assets/img/dubble/icon_grade_04.png">
                                <em>24{{this.$t('public.home.hours')}}</em>
                            </div>
                            <div class="grade_time_in">
                                <img src="../../../assets/img/dubble/icon_grade_05.png">
                                <em>7{{this.$t('public.home.day')}}</em>
                            </div>
                            <div class="grade_time_in">
                                <img src="../../../assets/img/dubble/icon_grade_06.png">
                                <em>30{{this.$t('public.home.day')}}</em>
                            </div>
                        </div>
                    </li>
                    <li>
                        <div class="grade_icon"><img src="../../../assets/img/dubble/icon_grade_03.png"></div>
                        <div class="grade_text">
                            <h2>{{this.$t('public.home.confidence')}}</h2>
                            <span><i>{{this.$t('public.home.community')}}</i><i>{{this.$t('public.home.passive')}}</i></span>
                        </div>
                    </li>
                </ul>
            </div>
            <div class="grade_project">
                <p>{{this.$t('public.home.investor')}}</p>
                <ul>
                    <li style="width: 100%;">
                        <div class="grade_icon"><img src="../../../assets/img/dubble/icon_grade_07.png"></div>
                        <div class="grade_text">
                            <h2>{{this.$t('public.home.individual')}}</h2>
                            <span><i>{{this.$t('public.home.transaction')}}</i><i>{{this.$t('public.home.assessment')}}</i><i>{{this.$t('public.home.transactions')}}</i><i>{{this.$t('public.home.total')}}</i><i>{{this.$t('public.home.risk')}}</i></span>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
        <Footer></Footer>
   </div>
</template>
<script>
import Header from '../../module/header'
import Footer from '../../module/footer'
export default {
  name: '',
  components: {
    Header,
    Footer
  },
  data () {
    return {

    }
  },
}
</script>
<style>
    .header{background: #000;}
	.grade{width: 100%; min-width:1200px; overflow: hidden; background:url(../../../assets/img/dubble/img_grade_bg.png) top no-repeat #000;font-family: "微软雅黑"; }
	.grade_banner{width:100%; height:273px; padding-top:95px;  background:url(../../../assets/img/dubble/img_grade_banner.png) center no-repeat; margin: 200px auto 20px auto; text-align: center;}
	.subheading i{font-style:normal;font-size: 20px; color: #000; background: #fff; padding: 5px 10px;}
	.maintitle i{font-style:normal;font-size: 58px; line-height: 90px; color: #fff;}
	.describe i{font-style:normal;font-size: 18px; color: #888;}
	.grade_introduce{width:1200px;font-size: 16px; text-align: center; line-height: 36px; color: #888; margin: 0px auto;}
	.grade_project{width:1200px; margin:150px auto;}
	.grade_project p{display:block; border-top: 1px solid #555; border-bottom: 1px solid #555; width: 200px; height: 50px; line-height: 50px; color: #fff; font-size: 24px; text-align: center; margin: 0px auto;}
	.grade_project ul{width: 1100px; list-style: none; padding:50px; overflow: hidden;}
	.grade_project ul li{width: 33.3%; float: left;}
	.grade_icon{width:48px; height: 48px; margin: 0px auto;}
	.grade_text{width:100%; text-align: center;}
	.grade_text h2{display: block; padding: 20px 0 0 0; margin: 0px; width:100%;font-size: 18px; color: #fff; text-align: center; font-family: "微软雅黑"; font-style: normal；}
	.grade_text span{display:block; width: 100%; overflow: hidden; color: #888; font-size: 14px; padding-top: 20px;}
	.grade_text span i{padding:0px 8px; font-style:normal;}
	.grade_time{width: 210px; margin: 30px auto 0px auto;}
	.grade_time_in{width: 70px; float: left; text-align: center;}
	.grade_time_in img{display:block; margin: 0px auto;}
	.grade_time_in em{display:block; font-style:normal;line-height: 30px; color: #888; font-size: 14px;}
</style>
