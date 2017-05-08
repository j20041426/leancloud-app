<template>
  <div class="page has-navbar" v-nav="{'title': '登录', showBackButton: true }">
    <div class="page-content padding padding-top">
      <von-input type="text" v-model="username" placeholder="用户名" label="用户名" floatingLabel="true"></von-input>
      <von-input type="password" v-model="password" placeholder="密码" label="密码" floatingLabel="true"></von-input>
      <md-button class="button button-positive button-block" @click.native="login()">登录</md-button>
    </div>
  </div>
</template>
<script>
  import axios from 'axios'
  import ERRORINFO from '../lib/errorinfo.js'
  
  export default {
    data () {
      return {
        username: '',
        password: ''
      }
    },
    methods: {
      login () {
        console.log('login');
        axios.post('http://app-fl2adar27dmfgvi.leanapp.cn/login',{
        //axios.post('http://localhost:3000/login',{
          "username": this.username,
          "password": this.password
        })
        .then(function(response){
          console.log(response);
          if(response.data.res == 0){
            $toast.show("登录成功", 2000);
          }else{
            $toast.show("登录失败:错误码"+response.data.msg, 2000);
          }
        })
        .catch(function(error){
          console.log(error);
        });
      }
    }
  }
</script>
<style scoped>
  body,html {
  	width: 100%;
  	height: 100%;
    font-family: '-apple-system', "Helvetica Neue", "Roboto", "Segoe UI", sans-serif;
  }
  * {
  	padding: 0;
  	margin: 0;
  }
  .button {
    margin-top: 50px !important;
  }
</style>
