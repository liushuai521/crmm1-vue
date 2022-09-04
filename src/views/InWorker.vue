<template>
  <div>
    编号:<input type="text" name="wid" v-model="id"/><br>
    姓名:<input type="text" name="wname" v-model="wname"/><br>
    性别:<input type="text" name="wsex" v-model="wsex"/><br>
    电话:<input type="text" name="wtel" v-model="iwtel"/><br>
    部门：<select width="600px" v-model="deptid">
       <option value="100" >请选择</option>
      <option value="100" v-for="(p,index) in plist" :key="index">请选择</option>
    </select>
    <br>
    <button @click="inWordker">提交</button>
  </div>
</template>

<script>
import axios from "axios"
  export default {
    name: "InWorker",
    data(){
     return {
      id:'',
      wname:'',
      wsex:'',
      iwtel:'',
      deptid:'',
      plist:[],
      }
    },
    methods:{
      inWordker(){
        axios.get("http://localhost:8888/inWorter?id="+this.id+'&wname='+this.wname+"&wsex"+this.wsex+"&wtel="+this.iwtel+"&deptid="+this.deptid).
        then(({data}) => {
          if(data!=0){
            this.$router.push("/index");
          }else{ 
            axios.get("修改失败")
          }
        })
      },
       up(w){
        axios.get("http://localhost:8888/").then(({data})=>{
          if(data!=0){
            alert("修改成功")
          }else{
            alert("修改失败")
          }
        })
      }
    }
  }
</script>

<style  scoped>

</style>