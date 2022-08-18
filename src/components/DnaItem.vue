<template>
  <div class="container"
    v-bind:class="{opacity: !visible}"
  >
    <div class="circle">
      <span class="text2" v-bind:class="{revert: revert}">P</span>
    </div>
    <div class="line"></div>
    <div class="line2"></div>
    <div class="pentagon"></div>
    <div class="hr"></div>
    <div class="pentagon2">
      <div class="containerText" v-bind:class="{revert: revert}">
        <span class="text">{{ item }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'DnaItem',
    props: {
      item: {
        required: true
      },
      revert: {
      }
    },
    data() {
        return {
            visible: false
        }
    },
    methods: {
      
    },
    mounted() {
      setTimeout(() => {
        this.visible = true
      }, 50);
    }
}
</script>
<style scoped>
.container{
  transition: opacity 0.2s ease;
  position: relative;
  widows: 100%;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
.opacity{
   opacity: 0;
}

.pentagon{
  clip-path: polygon(50% 8%, 100% 50%, 75% 100%, 25% 100%, 0 50%);
  width: 100px;
  height: 100px;
  background: sandybrown;
}
.pentagon2{
  clip-path: polygon(100% 20%, 80% 50%, 100% 80%, 0 80%, 0 20%);
  width: 100px;
  height: 100px;
  background: greenyellow;
}
.hr{
  border-top: 1px solid black;
  width: 30px;
}
.text{
  font-size: x-large;
  position: relative;
  top: calc(50% - 30px / 2);
  display: flex;
  justify-content: center;
  line-height: 30px;
}
.text2{
  font-size: x-large;
  position: relative;
  top: calc(24% - 30px / 2);
  right: 24%;
  display: flex;
  justify-content: center;
  line-height: 30px;
}
.revert{
  transform: scale(-1, 1);
}
.containerText{
  position: relative;
  width: 100%;
  height: 100%;
}
.circle{
  clip-path: circle(25.0% at 25% 25%);
  width: 100px;
  height: 100px;
  background: yellow;
}
.line{
  clip-path: polygon(0 0, 100% 99%, 100% 100%, 0 1%);
  width: 100px;
  height: 100px;
  background: black;
  position: absolute;
  left: 20px;
  top: -10px;
  z-index: -1;
  transform: rotate(-20deg);
}
.line2{
  clip-path: polygon(0 0, 100% 99%, 100% 100%, 0 1%);
  width: 100px;
  height: 60px;
  background: black;
  position: absolute;
  left: 20px;
  top: 76px;
  
  z-index: -1;
  transform: rotate(140deg);
}
</style>