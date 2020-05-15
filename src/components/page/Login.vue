<template>
  <div class="login-root">
    <div class="login-main">
      <div class="title">后台管理系统</div>
      <el-form :model="param" :rules="rules" ref="login" label-width="0px" class="content">
        <el-form-item prop="username">
          <el-input v-model="param.username" placeholder="username">
            <el-button slot="prepend" icon="el-icon-user"></el-button>
          </el-input>
        </el-form-item>
        <el-form-item prop="password">
          <el-input type="password" placeholder="password" v-model="param.password" @keyup.enter.native="submitForm">
            <el-button slot="prepend" icon="el-icon-lock"></el-button>
          </el-input>
        </el-form-item>
        <div class="btn-login">
          <el-button type="primary" @click="submitForm">登录</el-button>
        </div>
        <p class="tips-login">Tips: 用户名和密码随便填。</p>
      </el-form>
    </div>
  </div>
</template>

<script>
    export default {
        name: "Login",
        data() {
          return {
            param: {
              username: 'admin',
              password: '123123'
            },
            rules: {
              username: [{ required: true, message: '请输入用户名', trigger: 'blur' }],
              password: [{ required: true, message: '请输入密码', trigger: 'blur' }]
            }
          };
        },
      methods: {
          submitForm() {
             this.$refs.login.validate(valid => {
               if (valid) {
                 this.$message.success('登录成功');
                 localStorage.setItem('m_username', this.param.username);
                 this.$router.push('/')
               }
               else {
                 this.$message.error('请输入账号和密码');
                 console.log('error submit!!!');
                 return false;
               }
             });
          }
      }
    }
</script>

<style scoped>
.login-root {
  position: relative;
  width: 100%;
  height: 100%;
  background-image: url("../../assets/img/login-bg.jpg");
  background-size: 100%;
}
.title {
  width: 100%;
  line-height: 50px;
  text-align: center;
  font-size: 20px;
  color: #fff;
  border-bottom: 1px solid #ddd;
}
.login-main {
  position: absolute;
  left: 50%;
  top: 50%;
  margin: -190px 0 0 -175px;
  width: 350px;
  border-radius: 5px;
  background: rgba(255, 255, 255, 0.3);
  overflow: hidden;
}

  .content {
    padding: 30px 30px;
    overflow-y: hidden;
  }
  .btn-login {
    text-align: center;
  }
  .btn-login button {
    width: 100%;
    height: 36px;
    margin-bottom: 10px;
  }
  .tips-login {
    font-size: 12px;
    line-height: 30px;
    color: #fff;
  }
</style>
