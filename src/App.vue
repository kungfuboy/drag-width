<template>
  <div id="app">
    <drag-width :leftWid="[200, 220, 500]" :rightWid="[250, 300, 500]">
      <template slot="left">
        <div class="div div1"></div>
      </template>
      <template slot="center">
        <div class="div div2"></div>
      </template>
      <template slot="right">
        <div class="div div3"></div>
      </template>
    </drag-width>
  </div>
</template>

<script>
import DragWidth from './components/DragWidth'
export default {
  name: 'app',
  components: {
    DragWidth
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 600px;
  border: 1px solid #ccc;
  .div {
    height: 100%;
    &.div1, &.div3 {
      background: #A5DEE4;
    }
    &.div2 {
      background: #FBE251;
    }
  }
}
</style>
