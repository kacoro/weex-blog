<template>
  <div class="wrapper">
    <image :src="logo" class="logo" />
    <text class="greeting">kacoro!</text>
    <HelloWorld/>
    <div class="up" @click="goToTop">
      <image class="img" src="https://img.alicdn.com/tps/TB1ZVOEOpXXXXcQaXXXXXXXXXXX-200-200.png" />
    </div>
  </div>
</template>

<script>

import HelloWorld from '@/components/HelloWorld'
const dom = weex.requireModule('dom') || {};
  const stream = weex.requireModule('stream') || {};
  const modal = weex.requireModule('modal') || {};
  const API = 'http://127.0.0.1:7001'
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
    }
  },
  //  created: function() {
  //     const self = this;
  //     stream.fetch({
  //       method: 'GET',
  //       url: API,
  //       type:'json'
  //     }, function(ret) {
  //       if(!ret.ok){
  //         modal.toast({
  //           message: 'Network Error!',
  //           duration: 3
  //         });
  //       }else{
  //         modal.toast({
  //           message: ret.data,
  //           duration: 3
  //         });
  //       }
  //     });
  //   }
}
</script>

<style scoped>
  .wrapper {
    justify-content: center;
    align-items: center;
  }
  .logo {
    width: 424px;
    height: 200px;
  }
  .greeting {
    text-align: center;
    margin-top: 70px;
    font-size: 50px;
    color: #41B883;
  }
  .message {
    margin: 30px;
    font-size: 32px;
    color: #727272;
  }
</style>
