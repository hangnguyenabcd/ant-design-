<template>
  <div class="homecome">
    <center>
      <p>This is home page</p>
    </center>
  </div>
</template>
<script>
export default {
  name:'homecome',
  data(){
    return{
 
    }
  },
   methods: {
      checkLogin () {
        if(!this.isLogin){
          this.$router.replace({ name: 'Login' })
       }
      },
      Login: function(){
          console.log(this.ga)
      },
      handle: function(e){
          console.log(e)
          this.isLogin = e
          console.log(this.isLogin)
      }
    }
}
</script>

