<template>
  <div class="wrapper">
    <text  class="page-email">登录</text>
    <div class="textbox">
      <text>邮箱:</text>
    </div>
    <input type="text" class="input" v-model="email"></input>
    <div class="textbox">
      <text>密码:</text>
    </div>
    <input type="password" class="input" @input="onChange"></input>
    <div class="textbox">
      
    </div>
    <text class="button" @click="submit">{{loading ? '提交中...' : '提交'}}</text>
  </div>
</template>

<script>
const storage = weex.requireModule('storage')
  const stream = weex.requireModule('stream') || {};
  const modal = weex.requireModule('modal') || {};
  const API = '/api/user/add';
  
  export default {
    data: function () {
      return {
        email: '',
        pwd: '',
        loading: false,
        csrf:''
      }
    },
    methods: {
      submit: function() {
        const {email, pwd, loading} = this;
        const self = this;
        console.log(email, pwd)
        if (!email || !pwd) {
          modal.toast({
            message: '邮箱和密码不能为空。',
            duration: 3
          });
          return;
        }
        if (loading) {return;}
        this.loading = true;
        storage.getItem('_csrf', (event) => {
          if (event.result === 'success') {
            this.csrf = event.data
          } else {
            modal.toast({ message: '获取csrfFAIL', duration: 1 })
          }
        })
        const body = JSON.stringify({email, pwd});
        
        stream.fetch({
          method: 'POST',
          url: API,
          headers:{
              'Content-type': 'application/json',
              'x-csrf-token':this.csrf
          },
          type:'json',
          body: body
        }, function(ret) {
          self.loading = false;
          
          if(!ret.ok){
            modal.toast({
              message: 'Network Error!',
              duration: 3
            });
          }else{
            modal.toast({
              message: '提交成功!' + body,
              duration: 3
            });
          }
        })
      },
      onChange: function(event){
        const value = event.value || '';
        
        this.pwd = value.trim();
      }
    }
  }
</script>

<style>
  .wrapper {
    padding: 30px;
  }
  .page-email {
    font-size: 60px;
    font-weight: bold;
    margin-bottom: 50px;
  }
  .input {
    margin-top: 10px;
    padding-top: 20px;
    padding-bottom: 20px;
    padding-left: 20px;
    padding-right: 20px;
    color: #666666;
    border-width: 2px;
    border-style: solid;
    border-color: #41B883;
    font-size: 36px;
  }
  .input:focus {
    border-color: #3399ff;
  }
  .textarea {
    margin-top: 10px;
    margin-bottom: 60px;
    padding-top: 20px;
    padding-bottom: 20px;
    padding-left: 20px;
    padding-right: 20px;
    color: #666666;
    border-width: 2px;
    border-style: solid;
    border-color: #41B883;
    font-size: 36px;
  }
  .textarea:focus {
    border-color: #3399ff;
  }
  .textbox {
    margin: 30px 0;
  }
  .button {
    height: 80px;
    line-height: 80px;
    background-color: #3399ff;
    color: #fff;
    border-radius: 4px;
    text-align: center;
  }
</style>