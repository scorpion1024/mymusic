<template>
    <div class='bot_btn_box'>
        <span class='icon_prev iconfont' @click="prev"></span>
        <span :class='(isStop?"icon_play":"icon_stop")+" iconfont"' @click='change'></span>
        <span class='icon_next iconfont' @click='next'></span>
    </div>
</template>
<script>
// @ is an alias to /src
// icon_play
export default {
    name: 'XXX',
    props:["isStop"],
    data() {
        return {}
    },
    methods: {
      change(){
        this.$emit('stop',!this.isStop)
      },
      prev(){
        this.$emit('prev')
      },
      next(){
        this.$emit('next')
      }
    },
    components: {
        
    }
}
</script>
<style lang="less">
  .bot_btn_box{
    position: fixed;
    bottom:0;
    width: 100%;
    height: 10vh;
    line-height: 10vh;
    background: rgba(0, 0, 0, 0.2);
    z-index: 200;
    text-align: center;
    color:#fff;
    span:nth-child(2){
      font-weight: 600;
    }
    span{
      font-size: 40px;
      margin: 0 5vw;

    }
  }
</style>