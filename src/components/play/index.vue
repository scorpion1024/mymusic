<template>
  <div
    class='play_box'
    :style="{backgroundImage:`url(${bg})`,color:'red'}"
  >
    <Record :img='img' @click="change" :isStop='isStop'></Record>
    <Lyric :lyric='lyric' :title='title' :currentTime='currentTime'></Lyric>
    <audio :src="music" ref='audio'></audio>
    <div class="timeCon" @mousedown="onSlider" @touchstart="onSlider">
      <div class="showTime cur">{{showCurTime}}</div>
      <el-slider v-model="currentTime" :max="max" :show-tooltip="false" @change="patrol" :format-tooltip="formatTooltip"></el-slider>
      <div class="showTime max">{{showMaxTime}}</div>
    </div>
    <BOTBTN @stop="change" @prev='prevFn' @next="nextFn" :isStop='isStop'></BOTBTN>
  </div>
</template>
<script>
// @ is an alias to /src
import { getMusic } from "@/api/api.js";
import Record from './record'
import Lyric from './lyric'
import BOTBTN from './btn'
export default {
  name: "play",
  data() {
    return {
      title: "",
      img: "",
      lyric: "",
      bg: "",
      music:'',
      currentTime:0,
      timer:null ,
      watchTime:null,
      isStop:true,
      idList:[1,2,3],
      idIndex:0,
      max:0,
      patrolSlider:0,
      showCurTime:'00:00',
      showMaxTime:'00:00',
    };
  },
  created() {
    this.getInfo(this.idList[this.idIndex]);
    var app = this
    document.onkeydown = function() {
        let key = window.event.keyCode
        if (key == 32) {
          app.change(!app.isStop)
        }
    }
    this.watchTime = setInterval(() => {
      if(typeof(this.$refs.audio.duration) == 'number'){
        this.max = this.$refs.audio.duration
        this.showMaxTime = this.formatSeconds(this.max)
      }
    }, 500);
  },
  components: {Record,Lyric,BOTBTN},
  methods: {
    getInfo(id) {
      let data = getMusic(id)
      this.bg = data.bg;
      this.img = data.img;
      this.lyric = data.lyric;
      this.title = data.title;
      this.music = data.music;
      this.currentTime = 0;
      this.timer = null ;
      this.isStop = true;
    },
    prevFn(){
      this.idIndex = (this.idIndex - 1) < 0 ? this.idList.length-1 : this.idIndex - 1;
      this.getInfo(this.idList[this.idIndex])
    },
    nextFn(){
      this.idIndex = (this.idIndex + 1) >= this.idList.length ? 0 : this.idIndex + 1;
      this.getInfo(this.idList[this.idIndex])
    },
    change(state){
      this.isStop = state
      if(!state){
        this.$refs.audio.play()
        this.updateTime()
      }else{
        this.$refs.audio.pause()
        clearInterval(this.timer)
      }
    },
    updateTime(){
      this.timer = setInterval(() => {
        this.currentTime = this.$refs.audio.currentTime
        this.showCurTime = this.formatSeconds(this.currentTime)
      }, 50);
    },
    onSlider(){
      clearInterval(this.timer)
    },
    formatTooltip(val){
      this.showCurTime = this.formatSeconds(val)
    },
    patrol(patrolSlider){
      this.currentTime = this.$refs.audio.currentTime = patrolSlider
      this.showCurTime = this.formatSeconds(this.currentTime)
      if(!this.$refs.audio.paused){
        this.updateTime()
      }
      if(this.currentTime >= this.$refs.audio.duration){
        this.change(true)
      }
    },
    formatSeconds(value) {
      let theTime = parseInt(value)
      let middle= 0
      let result = '00:00'
      if(theTime > 60) {
        middle= parseInt(theTime/60);
        theTime = parseInt(theTime%60);
      }
      if(parseInt(theTime)<=9){
        theTime = "0"+theTime
      }
      if(parseInt(middle)<=9){
        middle = "0"+middle
      }
      result = middle+":"+theTime;
      return result;
    } 
  },
  watch: {
    max(cur) {
      if(cur>0){
        clearInterval(this.watchTime)
      }
    }
  },
};
</script>
<style lang="less">
.play_box {
  width: 100%;
  height: 100vh;
  background-size: auto 100%;
  background-position: center center;
  transform-origin: center top;
  &::before {
    content: " ";
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background-color: rgba(0, 0, 0, 0.5);
  }
}
.timeCon{
  padding: 0vh 10vw;
  position: relative;
}
.showTime{
  color: white;
  display: inline-block;
  font-size: 12px;
  position: absolute;
}
.max{
  right: 0;
  top: 0;
}
.cur{
  left: 0;
  top: 0;
}
</style>