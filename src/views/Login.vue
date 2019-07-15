<template>
  <a-form
    id="components-form-demo-normal-login"
    :form="form"
    class="login-form"
    @submit="handleSubmit"
  >
  <h1>LOGIN</h1>
    <a-form-item>
      <a-input
        v-decorator="[
          'userName',
          { rules: [{ required: true, message: 'Please input your username!' }] }
        ]"
        placeholder="Username"
        v-model="user.username"
      >
        <a-icon
          slot="prefix"
          type="user"
          style="color: rgba(0,0,0,.25)"
        />
      </a-input>
    </a-form-item>
    <a-form-item>
      <a-input
        v-decorator="[
          'password',
          { rules: [{ required: true, message: 'Please input your Password!' }] }
        ]"
        type="password"
        placeholder="Password"
        v-model="user.password"
      >
        <a-icon
          slot="prefix"
          type="lock"
          style="color: rgba(0,0,0,.25)"
        />
      </a-input>
    </a-form-item>
    <a-form-item>
      <a-checkbox
        v-decorator="[
          'remember',
          {
            valuePropName: 'checked',
            initialValue: true,
          }
        ]"
      >
        Remember me
      </a-checkbox>
      <a-button
        type="primary"
        html-type="submit"
        class="login-form-button"
        @click="clicked"
      >
        Log in
      </a-button>
    </a-form-item>
  </a-form>
</template>

<script>
import UsersRepository from './../service/UsersRepository'
export default {
  beforeCreate () {
    this.form = this.$form.createForm(this);
  },
  data(){
    return{
      user:{
        username: '',
        password:''
      },
      msgErrorText:''
    }
  },
  methods: {
     clicked: function () {
        UsersRepository.Login(this.user).then(res=>{
        if(res) {
        this.$emit("login-success",true)
         this.$emit("login-name",this.user.username)
        this.$router.replace({ name: 'home' })
      } else {
        this.msgErrorText="username and password are wrong, please re-enter"
      }
    })
  },
    handleSubmit (e) {
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log('Received values of form: ', values);
        }
      });
    },
  },
};
</script>
<style>
#components-form-demo-normal-login .login-form {
  max-width: 300px;
}
#components-form-demo-normal-login .login-form-forgot {
  float: right;
}
#components-form-demo-normal-login .login-form-button {
  width: 100%;
}
</style>