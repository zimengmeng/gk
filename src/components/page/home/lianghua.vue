<template>
    <div>
        <Header class="header"></Header>
        <div class="quantification">
            <div class="quantification_banner">
            <div class="banner_subheading">{{this.$t('public.lianghua.personal')}}</div>
            <div class="banner_subheading_en">One-stop Customizable Quantitative Investment Tool for Individual Investors</div>
            <div class="banner_title">{{this.$t('public.lianghua.investment')}}</div>
            <div class="banner_subheading_foot">{{this.$t('public.lianghua.eyes')}}</div>
        </div>
        
        <div class="quantification_contact">{{this.$t('public.lianghua.email')}}：EVEN@GK.COM</div>
        
        <div class="cion_max">
            <ul>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_01.png"></span>
                    <em>{{this.$t('public.lianghua.private')}}</em>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_02.png"></span>
                    <em>{{this.$t('public.lianghua.fund')}}</em>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_03.png"></span>
                    <em>{{this.$t('public.lianghua.pyramid')}}</em>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_04.png"></span>
                    <em>{{this.$t('public.lianghua.support')}}</em>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_05.png"></span>
                    <em>{{this.$t('public.lianghua.root')}}</em>
                </li>
            </ul>
        </div>
        
        <div class="quantification_content">
            <ul>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_07.png"></span>
                    <em>{{this.$t('public.home.deploy')}}</em>
                    <i>{{this.$t('public.home.deploys')}}</i>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_08.png"></span>
                    <em>{{this.$t('public.home.private')}}</em>
                    <i>{{this.$t('public.home.privates')}}</i>
                </li>
                <li style="width: 399px;">
                    <span><img src="../../../assets/img/lianghua/icon_quantification_09.png"></span>
                    <em>{{this.$t('public.home.circulation')}}</em>
                    <i>{{this.$t('public.home.circulations')}}</i>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_10.png"></span>
                    <em>{{this.$t('public.home.light')}}</em>
                    <i>{{this.$t('public.home.lights')}}</i>
                </li>
                <li>
                    <span><img src="../../../assets/img/lianghua/icon_quantification_06.png"></span>
                    <em>{{this.$t('public.lianghua.ai')}}</em>
                    <i>{{this.$t('public.lianghua.ais')}}</i>
                </li>
                <li style="width: 399px;">
                    <span><img src="../../../assets/img/lianghua/icon_quantification_11.png"></span>
                    <em>{{this.$t('public.lianghua.protection')}}</em>
                    <i>{{this.$t('public.lianghua.protections')}}</i>
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
    .quantification{width: 100%; min-width:1200px; overflow: hidden; background:url('../../../assets/img/lianghua/img_quantification_bg.png') top no-repeat #000;font-family: "微软雅黑"; }
	.quantification_banner{width:100%; height:273px; padding-top:110px;  background:url('../../../assets/img/lianghua/img_quantification_banner.png') center no-repeat; margin: 200px auto 20px auto; text-align: center; overflow: hidden;}
	.banner_subheading{font-size:20px; color: #fff;}
	.banner_subheading_en{font-size: 12px; color: #888;}
	.banner_title{font-size: 62px; line-height: 100px; color:#fff;}
	.banner_subheading_foot{font-size: 14px; line-height: 30px; color: #888;}
	.quantification_contact{width:100%; text-align: center; line-height: 80px; color: #fff; font-size: 16px;}
	.cion_max{width:1200px; margin: 0px auto 0px auto; overflow: hidden;}
	.cion_max ul{list-style:none;width:1200px;}
	.cion_max ul li{ width:240px;float: left; text-align: center;}
	.cion_max ul li span{display:block;}
	.cion_max ul li em{display:block; color: #fff; font-style:normal;font-size: 14px;}
	.quantification_content{width:1198px; margin: 200px auto 200px auto; background: #111; border-left: 1px solid #222222; border-top: 1px solid #222222; overflow: hidden;}
	.quantification_content ul{width:1198px; overflow: hidden; list-style: none; padding: 0px; margin: 0px;}
	.quantification_content ul li{float:left; width: 398px; border-bottom: 1px solid #222222; border-right:1px solid #222222;overflow: hidden; list-style: none}
	.quantification_content ul li span{display:block; width: 40px; padding: 30px 20px 10px 30px;}
	.quantification_content ul li em{display:block; font-style: normal; font-size: 18px; color: #fff;  padding: 10px 10px 0px 30px;}
	.quantification_content ul li i{display:block; font-style: normal; font-size: 14px; color: #888;  padding: 10px 10px 30px 30px;}
</style>