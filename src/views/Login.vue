<template>
 <div>
    账号:<input type="text" name="loginname" v-model="loginname" />
    <br />
    密码:<input type="text" name="loginpwd" v-model="loginpwd"/> <br /><br />
    <button type="button" name="submit" id="btn" @click="login">登入</button>
     <input type="button" value="重置" @click="cz"/>
    <br />
  </div>
</template>

<script>
import axios from "axios"
export default {
  name: "Login",
  data() {
    return {
      loginname: null,
      loginpwd: null,
    };
  },
    methods:{
            login(){
              
               const login ={
                    lname:this.loginname,
                    lpwd:this.loginpwd,   
                }
                var query = `?loginname=${login.lname}&loginpwd=${login.lpwd}`
                console.log(login);
                axios.get('http://localhost:8888/login'+query)
                    .then(resp=>{
                       console.log(resp.data);
                      var rs =  resp.data;
                      if(rs == null){
                        //  this.$message.error('登陆信息错误，请重新输入');
                        alert("登入失败");
                      }else{   
                            sessionStorage.setItem("name",rs.lName);
                            sessionStorage.setItem("loginname", rs.loginName);
                            this.$router.push("/index");
                             alert("登入成功");
                         
                     }
                    }).catch(function (error) {
                        console.log(error);
                    })
            },
            cz(){
          console.log("chongzhi")
                this.loginname = '';
                this.loginpwd = '';
            },
        },
         
};
</script>

<style  scoped>
</style>