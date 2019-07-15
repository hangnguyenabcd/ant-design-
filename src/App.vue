<template>
  <div id="app">
    <a-layout id="components-layout-demo-custom-trigger">
    <a-layout-sider
      :trigger="null"
      style="height: -webkit-fill-available"
      collapsible
      v-model="collapsed"
    >
      <div class="logo" />
      <a-menu theme="dark" mode="inline" :defaultSelectedKeys="['1']">
        <a-menu-item key="1">
          <a-icon type="user" />
          <span>Home</span>
        </a-menu-item>
        <a-menu-item key="2">
          <a-icon type="video-camera" />
          <span>Employee Manager </span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <a-layout>
      <a-layout-header style="background: #fff; padding: 0">
        <a-icon
          class="trigger"
          :type="collapsed ? 'menu-unfold' : 'menu-fold'"
          @click="()=> collapsed = !collapsed"
        />
        <button v-if="isLogin" @click="logout"><span>Log out</span></button>
      </a-layout-header>
      <a-layout-content :style="{ margin: '24px 16px', padding: '24px', background: '#fff', minHeight: '280px' }">
      
      <div v-if="!isLogin"><Login @login-success="loginsuccess" @loginname="loginname"/></div>
      </a-layout-content>
    </a-layout>
  </a-layout>
  </div>
</template>
<script>
import Login from './views/Login'
export default {
  name:'App',
  components:{
    Login
  },
  created(){
     if(this.isLogin == false){
      this.$router.replace({name: 'home'})
    }
  },
  data(){
    return {
      collapsed: false,
      isLogin: false,
      name: ''
    }
  },
  methods:{
  loginsuccess(e){
    this.isLogin=e
  },
  logout(){
    this.isLogin=!this.isLogin
    this.$router.replace({name: 'home'})
    this.name = ''
  },
  loginname(name){
    this.name= name;
  }
}
}
</script>
<style>
#components-layout-demo-custom-trigger .trigger {
  font-size: 18px;
  line-height: 64px;
  padding: 0 24px;
  cursor: pointer;
  transition: color .3s;
}

#components-layout-demo-custom-trigger .trigger:hover {
  color: #1890ff;
}

#components-layout-demo-custom-trigger .logo {
  height: 32px;
  background: rgba(255,255,255,.2);
  margin: 16px;
}
</style>
