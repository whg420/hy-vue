<template>

    <el-container>
  <el-aside width="200px">
    <ul v-for="(item,index) in list" :key="index">
      <li>{{item}}</li>
    </ul>
  </el-aside>
  <el-container>
    <el-header>会议室预定系统</el-header>
    <el-main>
      <p>操作提示:筛选会议室之后,在日历中可直接框选时间段预定或提交申请</p>
      <ul>
<li>{{data[0]}}</li>
<!-- <li>{{data[0].building}}</li>
<li>{{data[0].floor}}</li> -->
      </ul>
      <ol>

      </ol>
    </el-main>
  </el-container>
</el-container>
  
</template>

<script>
import axios from 'axios'
  export default {
    data() {
      return {
        list:[],
        data:[]
      }
    },
    mounted() {
      const code=this.$route.query.code;
       axios.get('/api/gets')
  .then( (response)=> {
    let data=response.data.data
    data.forEach(item => {
      if(item.code==this.$route.query.code){
        this.list=item;
      }
    });

  })
  .catch( (error)=> {
    // handle error
    console.log(error);
  })
  .then( ()=>{
    // always executed
  });
   axios.get('/api/getd')
  .then( (response)=> {
    // handle success
    // this.data=response.data.data;
    let data=response.data.data
    console.log(data[0],'--------------');
    this.data=data
    console.log(this.data);
    
  })
    },
  }
</script>

<style lang="scss" scoped>
.el-container{
    width: 100%;
    height: 100%;
}
.el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
  }
  .el-aside>ul{
    height: 40px;
  }
  .el-aside>ul>li{
    list-style: none;
  }
  .el-main {
    background-color: #E9EEF3;
    color: #333;
  }

  
  body > .el-container {

    margin-bottom: 40px;
  }
  
  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
</style>