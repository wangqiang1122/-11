<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>axios</h2>
  </div>
</template>

<script>
  import axios from "axios"
  let Http=axios.create({
    baseURL:"http://api.rrslj.com/v4/",//总路径
    timeout:1000,
    params:{},//查询字符串功能
    header:{}//设置请求头
  });
export default {
  name: 'HelloWorld',
  data :function() {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  created:function(){
    Http.get("index.php?act=goods&op=j_goods_detail&goods_id=234").then(function(res){console.log(res)}).catch(function(err){console.log(err)})
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
