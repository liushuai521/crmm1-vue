<template>
  <div id="box">
    <div id="zuo">
      <h3>用户菜单</h3>
      <button @click="dept(教学部)" value="教学部">教学部</button>
      <br>
      <button @click="dept()" value="市场部">市场部</button>
      <br>
      <button @click="dept()" value="就业部">就业部</button>
    </div>
     <div id="you">
      全选<input type="radio" name=""/>
      <table>
        <tr>
          <th>选择</th>
          <th>编号</th>
          <th>姓名</th>
          <th>性别</th>
          <th>电话号</th>
          <th>操作</th>
        </tr>
        <tr v-for="(w,index) in wlist" :key="index">
          <th><input type="radio" name=""></th>
          <th>{{w.id}}</th>
          <th>{{w.wname}}</th>
          <th>{{w.wsex}}</th>
          <th>{{w.wtel}}</th>
          <th><router-link to="/inWorker">修改</router-link>
            <button @click="del(w)">删除</button></th>
        </tr>
      </table>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import axios from "axios"
  export default {
    name:"index",
    data(){
      return {
      wlist:[]
      }
    },
    created(){
      this.getWorkerList();
    },
    methods:{
      getWorkerList(){
        var ulr = "http://localhost:8888/index"
        axios.get(ulr).then(({data})=>{
          console.log(ulr)
          this.wlist = data;
        })
      },

      dept(e){
        console.log(1,e ,2,this.html)
        var ulr = "http://localhost:8888/dept?dname="+this.html;
        axios.get(ulr).then(({data})=>{
          console.log(ulr)
          this.wlist = data;
        })
      },
      //删除
      del(id){
        axios.delete("http://localhost:8888/deleWorter?id="+id).then(({data})=>{
          if(data!=0){
            alert("删除成功")
          }else{
            alert("删除失败")
          }
        })
      },
     
    }
  }
</script>

<style scoped>
#box {
  display:flex;
}
#zuo{
  width: 200px;
  background-color: rgb(22, 192, 87);
}
#you{
   width: 500px;
   background-color: rgb(99, 221, 38);
}
</style>