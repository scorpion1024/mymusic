<template>
  <div class="load">
    <div>G</div>
    <div>N</div>
    <div>I</div>
    <div>D</div>
    <div>A</div>
    <div>O</div>
    <div>L</div>
  </div>
</template>
<script>
// @ is an alias to /src
export default {
  name: "Loading",
  data() {
    return {};
  },
  components: {}
};
</script>
<style lang="less">
.load {
  position: absolute;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  left: 50%;
  top:0;
  transform: translateX(-50%);
  user-select: none;
  cursor: default;
  background: rgba(240, 24, 24, 0.69);
  div {
    position: absolute;
    top:40%;
    font-size: 25px;
    width: 20px;
    height: 36px;
    opacity: 0;
    font-family: Helvetica, Arial, sans-serif;
    animation: move 2s linear infinite;
    transform: rotate(180deg);
    color: #fff;
    &:nth-child(2) {
      animation-delay: 0.2s;
    }
    &:nth-child(3) {
      animation-delay: 0.4s;
    }
    &:nth-child(4) {
      animation-delay: 0.6s;
    }
    &:nth-child(5) {
      animation-delay: 0.8s;
    }
    &:nth-child(6) {
      animation-delay: 1s;
    }
    &:nth-child(7) {
      animation-delay: 1.2s;
    }
  }
}
@keyframes move {
  0% {
    left: 0;
    opacity: 0;
  }
  35% {
    left: 30%;
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
    opacity: 1;
  }
  65% {
    left: 60%;
    -moz-transform: rotate(0deg);
    -webkit-transform: rotate(0deg);
    -o-transform: rotate(0deg);
    transform: rotate(0deg);
    opacity: 1;
  }
  100% {
    left: 100%;
    -moz-transform: rotate(-180deg);
    -webkit-transform: rotate(-180deg);
    -o-transform: rotate(-180deg);
    transform: rotate(-180deg);
    opacity: 0;
  }
}
</style>