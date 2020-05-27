<template>
  <div class='lyric_box'>
    <div class="til">{{title}}</div>
    <div class="lyric" ref="scollBox">
      <div class="lyric_list">
        <p
          v-for='(item,index) in lyricAry'
          ref='p'
          :key='index'
          :class='{active:activeIndex == index}'
        >{{item[1]}}</p>
      </div>
    </div>

  </div>
</template>
<script>
// @ is an alias to /src
export default {
  name: "Lyric",
  props: ["lyric", "title", "currentTime"],
  data() {
    return {
      moveY: 0
    };
  },
  mounted () {
    this.$refs.scollBox.addEventListener('scroll', () => {
      
    }, false)
  },
  computed: {
    lyricAry() {
      let str = this.lyric;
      let ary = [];
      str.replace(/\[(\d+):(\d+)\.(\d+)\] *([^\n]+)/g, function(a, b, c, d,e) {
        ary.push([b * 60 + c * 1 + d/1000, e]);
      });
      return ary;
    },
    activeIndex() {
      let temp = 0;
      let bol = this.lyricAry.some((item, index) => {
        temp = index;
        return this.currentTime <= item[0];
      });
      return bol ? temp - 1 : this.lyricAry.length-1;
    }
  },
  watch: {
    activeIndex(cur,old) {
      if(cur<3)return;
      let el = this.$refs.p[cur];
      if (el) {
        this.$refs.scollBox.scrollTop = cur*32
      }
    },
    lyricAry(){
      this.moveY = 0;
    }
  },
  methods: {
  },
  destroyed () {
    
  },
  components: {}
};
</script>
<style lang="less">
.lyric_box {
  color: #fff;
  position: relative;
  font-size: 1em;
  height: 45vh;
  overflow: hidden;
  text-align: center;
  .til {
    height: 6vh;
    padding-top: 2vh;
  }
  .lyric {
    height: 36vh;
    color: #b3b0b0;
    overflow: scroll;
  }
  p {
    padding: 1vh;
  }
  p.active {
    color: #fff;
  }
}
::-webkit-scrollbar {
  display: none; /* Chrome Safari */
}
</style>