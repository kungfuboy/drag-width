<template>
  <section
    ref="dragWidth"
    class="drag-width"
    @mousemove="handleMouseMove($event)"
    @mouseup="handleMouseUp()"
  >
    <section :style="{ width: `${lw}px` }" class="left">
      <slot name="left"></slot>
    </section>
    <i class="splitpane" @mousedown.prevent="handleMouseDown('left')"></i>
    <section class="center">
    <slot name="center"></slot></section>
    <i class="splitpane" @mousedown.prevent="handleMouseDown('right')"></i>
    <section :style="{ width: `${rw}px` }" class="right">
      <slot name="right"></slot>
    </section>
  </section>
</template>
<script>
// 改变比例宽度的开关
let isHandleLeft = false
let isHandleRight = false
let WIDTH = 0
let LEFTWID = 0
export default {
  props: {
    leftWid: {
      type: Array,
      default: () => {}
    },
    rightWid: {
      type: Array,
      default: () => {}
    }
  },
  data () {
    return {
      lw: 0,
      rw: 0
    }
  },
  mounted () {
    WIDTH = this.$refs.dragWidth.clientWidth
    LEFTWID = this.$refs.dragWidth.getBoundingClientRect().left
    this.lw = this.leftWid[1]
    this.rw = this.rightWid[1]
  },
  methods: {
    handleMouseDown (type) {
      if (type === 'left') {
        isHandleLeft = true
        return
      }
      if (type === 'right') {
        isHandleRight = true
      }
    },
    handleMouseMove (e) {
      if (isHandleLeft) {
        const lw = e.clientX < this.leftWid[2] + LEFTWID ? e.clientX - LEFTWID : this.leftWid[2]
        this.lw = lw > this.leftWid[0] ? lw : this.leftWid[0]
        return
      }
      if (isHandleRight) {
        const rw =
          WIDTH - e.clientX < this.rightWid[2] - LEFTWID
            ? WIDTH - e.clientX + LEFTWID
            : this.rightWid[2]
        this.rw = rw > this.rightWid[0] ? rw : this.rightWid[0]
      }
    },
    handleMouseUp () {
      isHandleLeft = isHandleRight = false
    }
  }
}
</script>
<style lang="less" scoped>
.drag-width {
    display: flex;
    height: 100%;
    .left, .right {
        flex-shrink: 0;
        height: 100%;
    }
    .center {
        flex: 1;
    }
    .splitpane {
      display: block;
      height: 100%;
      width: 5px;
      background: #888;
      cursor: move;
      flex-shrink: 0;
    }
}
</style>
