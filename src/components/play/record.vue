<template>
  <div class='record_box' @click='click'>
    <div
      class="record"
      :class='{stop:isStop}'
    >
      <img
        :src="img"
        alt=""
      >
      <div class="record_bg"></div>
    </div>
    <div class="btn" v-show='isStop'></div>
  </div>
</template>
<script>
// @ is an alias to /src
export default {
  name: "Record",
  props: ["img",'isStop'],
  data() {
    return {
      stop: "stop"
    };
  },
  methods: {
    click() {
			this.$emit('click',!this.isStop)
    }
  },
  components: {}
};
</script>
<style lang="less">
.record_box {
  position: relative;
  height: 42vh;
  &::before {
    content: "";
    display: block;
    width: 30vw;
    height: 30vw;
    position: absolute;
    background-image: url("../../assets/imgs/needle.png");
    background-size: contain;
    background-repeat: no-repeat;
    left: 45%;
    z-index: 100;
  }
  .record {
    width: 60vw;
    height: 60vw;
    position: relative;
    z-index: 20;
    margin: auto;
    top: 15vw;
    animation: rotateMove 4s linear infinite;
    img {
      position: absolute;
      width: 80%;
      height: auto;
      border-radius: 50%;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
    }
    .record_bg {
      position: relative;
      width: 100%;
      height: 100%;
      top: 0;
      background-image: url("../../assets/imgs/circle.png");
      background-position: center center;
      background-size: contain;
    }
  }
  .stop {
    animation-play-state: paused;
  }
  .btn {
		position: absolute;
		z-index: 120;
    width: 15vw;
    height: 15vw;
    left: 50%;
    top: 37vw;
    transform: translate(-50%,0);
		background: url('../../assets/imgs/play_btn.png') no-repeat center center;
		background-size: contain;
  }
  @keyframes rotateMove {
    0% {
      transform: rotate(0);
    }
    100% {
      transform: rotate(360deg);
    }
  }
}
</style>