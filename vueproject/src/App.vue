<template>
  <div class="login">
    <el-container>
      <el-main>
        <div class="form_container" style="background-color: azure">
          <el-form :model="data" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-form-item label="帐号" prop="account">
                <el-input v-model="data.account"></el-input>
            </el-form-item>
            <el-form-item label="密码" prop="password">
              <el-input v-model="data.password" type="password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submitForm('data')">登录</el-button>
            </el-form-item>
          </el-form>
        </div>
      </el-main>
    </el-container>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        data: {
          account: '',
          password: ''
        },
        rules: {
          account: [
            { required: true, message: '请输入帐号', trigger: 'blur' },
            { min: 5, max: 15, message: '长度在 5 到 15 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'change'}
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
		//alert("submit");
        var formData = JSON.stringify(this.data); // 这里才是你的表单数据
 
          this.$http.jsonp('http://liaojianbin.top:8081/hello/sayHello', {
			params: {},
			jsonp: 'onBack'
		  }).then((response) => {
              // success callback
              console.log(response.data);
			  alert(response.data);
          }, (response) => {
               console.log("error");
			   alert(response.data);
			   alert(formData);
              // error callback
          });
      }
    }
  }
</script>
<style>
  .form_container {
    -webkit-border-radius: 5px;
    border-radius: 5px;
    -moz-border-radius: 5px;
    background-clip: padding-box;
    margin: 180px auto;
    width: 350px;
    padding: 35px 50px 15px 25px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }
</style>