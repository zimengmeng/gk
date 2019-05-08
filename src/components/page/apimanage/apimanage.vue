<template>
    <div class="apimanage"> 
      <Header></Header>
      <div class="api">
             <div class="api-main">
                <div class="api-main-content" >
                  <!-- <ul class="api-tab ">
                      <li :class="{selected:myapi}" @click="apiTag('Myapi')">{{$t('user.api.myapi')}}</li>
                      <li @click="apiTag('apidoc')" :class="{selected:apidoc}">{{$t('user.api.apidocd')}}</li>
                  </ul> -->
                  <h1>{{$t('user.api.myapi')}}</h1>
                  <Myapi></Myapi>
                  <Apidoc></Apidoc>
                </div>
            </div>
    </div>
     <Footer></Footer>
  </div>
</template>
<script lang="js">
// 我的APi组建
import Myapi from '@/components/page/apimanage/myapi'
// Api文档
import Apidoc from '@/components/page/apimanage/apidoc'
import Header from '../../module/header'
import Footer from '../../module/footer'
export default {
  name: 'apimanage',
  components: {
    Myapi,
    Apidoc,
    Header,
    Footer
  },
  mounted () {

  },
  data () {
    return {
      mainHeight: 0,
      myapi: true,
      apidoc: false,
      current: 'Myapi'
    }
  },
  methods: {
    apiTag: function (tag) {
      this.current = tag
      if (tag === 'Myapi') {
        this.myapi = true
        this.apidoc = false
      } else {
        this.myapi = false
        this.apidoc = true
      }
    }
  },
  computed: {}

}
</script>

<style lang="stylus" scoped>

</style>
