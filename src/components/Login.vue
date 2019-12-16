<template>
  <div class="login-container">
    <!-- logo区域 -->
    <div class="logo">
      <a href="" target="_blank">
        <img src="../assets/image/heima_logo.png" alt="">
      </a>
    </div>
    <!-- 登录的表单 -->
    <el-form :model="loginForm" :rules="loginFormRules" ref="loginFormRef" label-width="0px" class="loginform_style">
      <!-- 登录名 -->
      <el-form-item prop="username">
        <el-input v-model="loginForm.username"
        placeholder="获取登录权限"
        >
          <!-- 使用 slot 为 输入框设置图标 -->
          <i slot="prefix" class="iconfont icon-user"></i>
        </el-input>
      </el-form-item>
      <!-- 登录密码 -->
      <el-form-item prop="password">
        <el-input v-model="loginForm.password" type="password" placeholder="点击logo图标，查看项目大图详情介绍">
          <i slot="prefix" class="iconfont icon-3702mima"></i>
        </el-input>
      </el-form-item>
      <el-form-item class="btns">
        <el-button type="primary" @click="login">登录</el-button>
        <el-button type="info" @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
    <!--  -->
    <div id="introduce">
      <!-- <a href="https://github.com/MarkSJun/BackStageManagement-/blob/master/README.md">点击查看项目介绍</a> display: flex;
    justify-content: center;-->
    </div>
    <span style="width: 100%;color: gray; position: fixed; bottom: 0; right: 0;font-size: 12px;text-align: center;">本课程由 </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 登录的表单绑定到的数据对象
      loginForm:{
        username:'',
        password:''
      },
      
      // 登录表单的验证规则 element.ui验证规则
      loginFormRules: {
        // 登录名的校验规则
        username: [
          { required: true, message: '请输入登录名称', trigger: 'blur' },
          { min: 3, max: 8, message: '长度在 3 到 8 个字符', trigger: 'blur' }
        ],
        // 登录密码的校验规则 
        password: [
          { required: true, message: '请输入登录密码', trigger: 'blur' },
          { min: 6, max: 50, message: '长度在 6 到 50 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  created() {
    var lett = this
    document.onkeydown = function(e) {
      var key = window.event.keyCode
      if (key === 13) {
        lett.login()
      }
    }
  },
  methods: {
    // 点击重置按钮，重置表单项
    resetForm() {
      this.$refs.loginFormRef.resetFields()
    },
    // 点击按钮登录
    login() {
      // 验证表单 async和await简化登陆请求代码异步ajax看起来像同步代码
      this.$refs.loginFormRef.validate(async valid => {
        // 验证失败，立即return
        if (!valid) return
        // 发起登录的请求
        const { data: res } = await this.$http.post('login', this.loginForm)
        // 登录失败
        if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
        // 登录成功
        this.$message.success(res.meta.msg)
        // 把登录成功后的令牌，保存到 sessionStorage， 供后续接口使用
        window.sessionStorage.setItem('token', res.data.token)
        // 使用 JS API 实现登录跳转   this.$router
        // 跳转到 后台主页
        this.$router.push('/home')
      })
    }
  }
}
</script>

<style scoped lang="less">
.login-container {
  width: 450px;
  height: 314px;
  background-color: #fff;
  position: absolute;
  top: 25%;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 5px;

  .logo {
    width: 130px;
    height: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 8px;
    box-shadow: 0 0 10px #eee;
    position: absolute;
    left: 50%;
    transform: translateX(-50%) translateY(-60px);
    background-color: #fff;

    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }

  .loginform_style {
    padding: 0 20px;
    margin-top: 110px;
  }

  .btns {
    display: flex;
    justify-content: center;
  }

  #introduce {
    position: absolute;
    top: 27%;
    width: 100%;
    text-align: center;
    a {
    text-decoration: none;
    }
  }
}
</style>
