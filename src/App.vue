<template>
  <div id="app">
    <transition name="fade">
      <component :is="showCom"></component>
    </transition>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Play from './components/play'
import Loading from './components/loading'
export default {
  name: 'App',
  data(){
    return{
      showCom:Loading
    }
  },
  created() {
    window.addEventListener('load',()=>{
      setTimeout(() => {
        this.showCom = Play;
      }, 500);
    })
  }
}
</script>

<style lang='less'>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
button{
  position: fixed;
  z-index: 19;
}


</style>
