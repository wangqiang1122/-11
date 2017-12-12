<template>
  <div id="app">
    <!--<img src="./assets/logo.png">-->
    <!--<router-view/>-->
    <vaildata :num="6"></vaildata>
  </div>
</template>


<script>
  import axios from "axios"
  import vaildata from "./components/vaildate1/index.vue"
  export default {
    name: 'app',
    components:{
      vaildata:vaildata
    },
    created:function(){
//      axios({
//        method:"post",
//        url:"http://api.rrslj.com/v4/index.php?act=goods&op=j_goods_detail&goods_id=2341&area=%E6%B1%9F%E8%8B%8F%7C%E5%8D%97%E4%BA%AC%E5%B8%82%7C%E7%8E%84%E6%AD%A6%E5%8C%BA%7C118.865851%2C32.030846"
//      }).then((res)=>{
//        console.log(res)
//      }).catch(function(err){
//        console.log(err)
//      })
//      axios.get("http://api.rrslj.com/v4/index.php?act=goods&op=j_goods_detail&goods_id=2341",{params:{name:"daad"}})
//        .then(function(res){console.log(res)}).catch(function(err){console.log(err)})
//      this.$http.get("http://api.rrslj.com/v4/index.php?act=goods&op=j_goods_detail&goods_id=2341").then(function(res){console.log(res)})
//        .catch(function(err){console.log(err)})

    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
