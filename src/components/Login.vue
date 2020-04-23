<template>
  <div class='login-container'>
      <div class="login-box">
          <!-- Avatar Start -->
          <div class="avatar-box">
              <img src="../assets/logo.png" alt="logo">
          </div>
          <!-- Avatar End -->
          <!-- Form Start -->
        <el-form class="login-form" ref= 'loginFormRef' :model= 'form' :rules="rules">
            <el-form-item prop="name">
                <el-input v-model= 'form.name' prefix-icon = "el-icon-user"></el-input>
            </el-form-item>
             <el-form-item prop="password">
                <el-input type="password" v-model= 'form.password' prefix-icon="el-icon-key"></el-input>
            </el-form-item>
             <el-form-item class="btns">
                <el-button type= 'primary' @click= 'login'>登录</el-button>
                <el-button type= 'info' @click = 'resetLoginForm'>重置</el-button>
            </el-form-item>
        </el-form>
          <!-- Form End -->
      </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      form: {
        name: '',
        password: ''
      },
      rules: {
        name: [
          { required: true, message: 'Please enter your username', trigger: true },
          { min: 3, max: 10, message: 'Must be 3 to 10 characters in length' }
        ],
        password: [
          { required: true, message: 'Please enter your username', trigger: true },
          { min: 3, max: 10, message: 'Must be 3 to 10 characters in length' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm () {
      // console.log(this.$refs)
      this.$refs.loginFormRef.resetFields()
    },
    login () {
      this.$refs.loginFormRef.validate((valid) => {
        if (!valid) return
        window.sessionStorage.setItem('token', this.randomString())
        this.$router.push('/home')
      })
    },
    // Create Random String
    randomString (len) {
      len = len || 32
      var $chars = 'ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz2345678'
      var maxPos = $chars.length
      var pwd = ''
      for (var i = 0; i < len; i++) {
        pwd += $chars.charAt(Math.floor(Math.random() * maxPos))
      }
      return pwd
    }
  }
}
</script>

<style lang='less' scoped>
.login-container{
    height: 100%;
    background-color: #2b4b6b;
    .login-box{
        position: absolute;
        width: 450px;
        height: 300px;
        border-radius: 3px;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: #fff;
        // ----- Avatar_Box Start -----
        .avatar-box{
            width: 130px;
            height: 130px;
            padding: 10px;
            background-color: #fff;
            border: 1px solid #eee;
            border-radius: 50%;
            position: absolute;
            left: 50%;
            transform: translate(-50%, -50%);
            img{
                max-width: 100%;
                height: auto;
                border-radius: 50%;
                background-color: #eee;
                display: block;
            }
        }
        // ----- Avatar_Box End -----
        // ----- Login_Form Start-----
        .login-form{
            position: absolute;
            bottom: 0;
            width: 100%;
            padding: 20px;
            box-sizing: border-box;
        }
        // ----- Login_Form End -----
        // ----- Btns Start-----
        .btns{
            display: flex;
            justify-content: flex-end;
        }
        // ----- Btns End -----
    }
}
</style>
