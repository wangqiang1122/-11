<template>
  <div>

      <div class="vaildate-v1" @click="clinpint">
        <div class="vaildate-v2" ref="vaildate" :style="{'z-index':zH}">
          <input type="tel"
                 @blur="outinput"
                 @keyup="outin"
                 v-focus
                 pattern="[0-9]*"
                 size="1"
                 v-model="messageNum"
                 maxlength="1"
                 @keyup.delete="outdelete"
                 ref="inputcode"
            />
        </div>
        <span   v-for="i in num" v-text="codeArray[i-1]?codeArray[i-1]:''" ref="spanlist" ></span>
      </div>

  </div>
</template>
<script>
  export default {
    props:{
      num:{ //有几个格子
        type:Number,
        default:6
      }
    },
    data:function(){
      return {
        index1:0,//记录索引
        inputCode: "", //单次输入的值
        codeArray:[],  //单次展示的值
        messageNum:"",//单次输入的值
        zH:10,//绝对定位层级
        blockWidth: (100/this.num).toFixed(4)+'%' ,//每个格子的宽度
        blockSize: (100/this.num).toFixed(4), //计算用宽度
      }
    },
    computed:{

    },
    mounted:function(){
      let Numwidth=this.$refs.spanlist[0];
      Numwidth.setAttribute("class","vaildateActive")
      this.$refs.inputcode.style.width=Numwidth.offsetWidth-10+"px"
    },
    methods:{
      convert:function(px){//px换算
         return (px/75)
      },
      outinput:function(){//失去焦点
        let listSpan=this.$refs.spanlist;
       this.zH=-10;
       let numlist=this.codeArray.join("");
        if(numlist.length<this.num){
          this.$emit("vaildate",{code:0,message:"验证码不正确"})
        }else{
          this.$emit("vaildate",{code:1,message:numlist})
        }
        listSpan[this.index1].setAttribute("class","")
      },
      clinpint:function(){//获去焦点
        let listSpan=this.$refs.spanlist;
        this.zH = 10;
        this.$refs.inputcode.focus();
        listSpan[this.index1].setAttribute("class","vaildateActive")
      },
      outdelete:function(){//删除
        let input1=this.$refs.vaildate;
        let listSpan=this.$refs.spanlist;
        if(this.codeArray.length==this.num){
          this.codeArray.pop();
         return
        }
        this.index1--;
        this.codeArray.pop();
        let n=this.index1<0?0:this.index1;
        this.index1=n;
        listSpan[this.index1+1].setAttribute("class","");
        listSpan[this.index1].setAttribute("class","vaildateActive")
        input1.style.left=(this.blockSize*n)+"%"
      },
      outin:function(){//按键抬起时
        if(!this.messageNum) return;
        if(this.messageNum==" "){
          this.messageNum="";
          return
        }
         let input1=this.$refs.vaildate;
         let listSpan=this.$refs.spanlist;
         ++this.index1;
        if(this.index1>=this.num){
          this.index1=this.num-1;
          this.codeArray[this.index1]=this.messageNum+"";
        }else{
          this.codeArray.push((this.messageNum+""));
          this.messageNum="";
          let Numwidth=this.$refs.spanlist[0].offsetWidth;
          input1.style.left=(this.blockSize*this.index1)+"%"
        }
        listSpan[this.index1-1].setAttribute("class","")
        listSpan[this.index1].setAttribute("class","vaildateActive")
      }
    },
    directives:{
      focus:{
        // 指令的定义
        inserted: function (el) {
          el.focus()
        }
      }
    }
  }
</script>
<style>
  .vaildate-v1{
    position: relative;
    margin-top: 50px;
    overflow: hidden;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
  }
  .vaildate-v2 {
    height: 80px;
    position: absolute;
  }
  .vaildate-v2 input{
    width: 90%;
    height: 90%;
    border: none;
    outline:none;
    text-align: center;
    margin-top: 10px;
    margin-left: 7px;
    font-size: 30px;
  }
  .vaildate-v1 span{
    float: left;
    height: 90px;
    line-height: 90px;
    border: 1px solid #000;
    border-left:none ;
    text-align: center;
    font-size: 30px;
    -webkit-box-flex: 1;
    -ms-flex: 1;
    flex: 1;
  }
  span:nth-child(2){
    border-left:1px solid #000;
 }
 .vaildate-v1-z{

 }
  .vaildate-v1-header{
    font-size: 30px;
  }
</style>