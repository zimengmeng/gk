<template>
   <div>
        <Header class="header"></Header>
        <div class="simulation">
            <div class="simulation_content">
                    <div class="simulation_title01">{{this.$t('public.simulation.free')}}  {{this.$t('public.simulation.simulation')}}</div>
                    <div class="simulation_title02">{{this.$t('public.simulation.system')}}</div>
                    <div class="simulation_title03">GK SIMULATION TRADING SYSTEM</div>
                    <div class="simulation_title04">{{this.$t('public.simulation.soon')}}</div>
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
  	.simulation{width: 100%; min-width:1200px; height: 1297px; background:url('../../../assets/img/simulation/img_simulation_bg.png') center no-repeat #000; font-family: "微软雅黑";}
	.simulation_content{color:#fff; width: 800px; position: fixed; top:300px; left: 50%; margin-left: -400px;}
	.simulation_title01{text-align: center; font-size: 18px; height: 40px; line-height: 40px; background:url('../../../assets/img/simulation/img_simulation_title.png') center no-repeat; }
	.simulation_title02{text-align: center; font-size: 88px; line-height: 160px;}
	.simulation_title03{text-align: center; font-size: 24px; color: #666;}
	.simulation_title04{text-align: center; font-size: 36px; line-height: 160px;}
</style>
