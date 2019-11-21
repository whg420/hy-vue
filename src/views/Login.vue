<template>
  <div>
    <ul>
      <li><input placeholder="请输入账号" type="text" id="username" v-model="ipt1"/></li>
      <li><input placeholder="请输入账号" type="password" id="password" v-model="ipt2"/></li>
      <li><button @click="ck">登录</button></li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
  export default {
  data() {
    return {
      ipt1:null,
      ipt2:null,
     data:[]
    }
  },
 methods: {
    ck(){
    console.log(this.ipt1);
    console.log(this.ipt2);
    let data=JSON.parse(JSON.stringify(this.data))
    console.log(data);

    let falg=data.some((item,index) => {
      return item.name==this.ipt1&&item.password==this.ipt2
    });
    if(falg){
    data.forEach(item => {
      if(item.name==this.ipt1){
        const code=Number(item.code);
        console.log(code);
      this.$router.push({path:"/home",query:{code}})       
        
      }
    });
    }else{
      alert('没有这个账户')
    }
  },
 },
  mounted() {
   axios.get('/api/get')
  .then( (response)=> {
    // handle success
    this.data=response.data.data;
  })
  .catch( (error)=> {
    // handle error
    console.log(error);
  })
  .then( ()=>{
    // always executed
  });
  },
  }
</script>

<style scoped>

</style>