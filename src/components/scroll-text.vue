<template>
  <div
    :style="{ width: containerWidth + 'px', height: containerHeight + 'px' }"
    class="scroll-container">
    <span
    ref="text"
      :style="{ transform: 'translateX(' + translateX + 'px)' }"
      class="scroll-text">
      {{ text }}
      </span>
  </div>
</template>

<script>
export default {
  name: "scrollText",
  props: {
    text: {
      type: String,
      default: "",
    },
    containerWidth: {
      type: Number,
      default: 200,
    },
    containerHeight: {
      type: Number,
      default: 50,
    },
    speed: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      textWidth: 0,
      translateX: 0,
      requestId: null,
    };
  },
  methods: {
    startScroll() {
      if (!this.requestId) {
      this.requestId = requestAnimationFrame(() => {
        this.scroll()
      })
    }
    },
    scroll() { 
      this.translateX -= this.speed
      if (this.translateX < - this.textWidth) {
        this.translateX += this.textWidth
      }
      this.$refs.text.style.transform = `translateX(${this.translateX}px)`
      this.requestId = requestAnimationFrame(() => this.scroll())
    },
    stopScroll() {
      clearInterval(this.requestId);
    },
  },
  mounted() {
    this.textWidth = this.$refs.text.offsetWidth
    this.text && this.startScroll();
  },
  beforeDestroy() {
    this.stopScroll();
  },
};
</script>
<style>
.scroll-container {
  position: relative;
  overflow: hidden;
  border: 1px solid #ccc;
  display: flex;
  align-items: center;
}

.scroll-text {
  position: absolute;
  white-space: nowrap;
  font-size: 14px;
  color: #333;
}
</style>

