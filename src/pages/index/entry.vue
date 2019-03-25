<template>
  <div class="wrapper">
    <image :src="logo" class="logo" />
    <text class="greeting">The environment is ready!</text>
    <Bar/>
    <Foo/>
  </div>
</template>

<script>
import Foo from '../../components/foo'
import Bar from './bar'
const storage = weex.requireModule('storage')
  const stream = weex.requireModule('stream') || {};
export default {
  name: 'App',
  components: {
    Foo,
    Bar
  },
  data () {
    return {
      logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
    }
  },
  created () {
    stream.fetch({
      method: 'GET',
      type: 'json',
      url: '/api/csrf'
    }, res => {
      console.log(res)
      if (res.ok) {
        storage.setItem('_csrf', res.data._csrf, () => {})
      } else {
        this.count = '- unknown -'
      }
    })
  }
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
