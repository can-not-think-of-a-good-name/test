<template>
  <div class="login-container">
    <div class="bg">
      <img :src="background">
    </div>
    <el-form :model="ruleForm2" :rules="rules2"
      status-icon
      ref="ruleForm2" 
      label-position="left" 
      label-width="0px" 
      class="demo-ruleForm login-page">
        <h3 class="title">{{Input}}</h3>
        <el-form-item prop="username">
          <el-input prefix-icon="el-icon-user" type="text" 
              v-model="ruleForm2.username" 
              auto-complete="off" 
              placeholder="用户名/手机号/邮箱"
          ></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input prefix-icon="el-icon-unlock" type="password" 
            v-model="ruleForm2.password" 
            auto-complete="off" 
            placeholder="密码"
            show-password
          ></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="handleSubmit" :loading="logining">登录</el-button>
        </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data(){
    return {
      background: require('../assets/bg.jpg'),
      Input:"Welcome !",
      Sign:"登录",
      logining: false,
      ruleForm2: {
        username: '',
        password: '',
      },
      rules2: {
        username: [{required: true, message: '请输入用户名', trigger: 'blur'}],
        password: [{required: true, message: '请输入密码', trigger: 'blur'}]
      },
      checked: false
    }
  },
  methods: {
    handleSubmit(event){
      this.$refs.ruleForm2.validate((valid) => {
        if(valid){
          this.logining = true;
          if(this.ruleForm2.username === 'admin' && 
              this.ruleForm2.password === '123456'){
                this.logining = false;
                sessionStorage.setItem('user', this.ruleForm2.username);
                this.$router.push({path: '/'});
            }else{
              this.logining = false;
              this.$alert('用户名密码错误', '提示', {
                confirmButtonText: '确认'
              })
          }
        }else{
          console.log('error submit!');
          return false;
        }
      })
    }
  }
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
}

.bg>img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.title{
  color: darkturquoise;
  font-size: 45px;
  text-align: center;
  margin-top: 45px;
  margin-bottom: 10px;
}

.login-page {
  position: absolute;
  left: 50%;
  top: 50%;
  margin-left: -375px;
  margin-top: -260px;
  width: 750px;
  height: 450px;
  background-color: rgba(135, 206, 235, .5);
  border-radius: 70px;
}

.el-input{
  width: 290px;
  height: 35px;
  margin-top: 50px;
  border: 0px solid rgba(255, 255, 255, .6);
  background-color: rgba(255, 255, 255, .6);
}

.el-button{
  position: absolute;
  width: 250px;
  height: 40px;
  margin-top: 80px;
  text-indent: 10px;
  border: 1px solid cyan;
  background-color: darkturquoise;
  cursor: pointer;
  color: white;
  font-size: 18px;
  text-align: center;
  left: 50%;
  margin-left: -125px;;
}

.el-form-item >>> .el-form-item__error {
  font-size: 18px;
  width: 290px;
  height: 35px;
  text-align: left;
  left: 50%;
  margin-left: -145px;
}
</style>