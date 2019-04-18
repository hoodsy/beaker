<template>
  <div class="s-spinner">
    <div class="s-bars" :size="size" :swap="swap">
      <svg
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
        :class="spinnerClass"
        viewBox="0 0 28 40"
      >
        <path d="M0 0, l0 4, l0 -4" id="s-bar-y-path"></path>
        <rect
          width="4"
          height="40"
          x="0"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar"
          :class="swapMode"
        >
        </rect>
        <rect
          width="4"
          height="40"
          x="12"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar middle"
          :class="swapMode"
        >
        </rect>
        <rect
          width="4"
          height="40"
          x="24"
          y="0"
          ry="2"
          rx="2"
          class="s-spinner__bar last"
          :class="swapMode"
        >
        </rect>
      </svg>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({})
export default class Spinner extends Vue {
  @Prop({ default: "small" })
  size!: String;

  @Prop({ default: false })
  swap!: Boolean;

  get spinnerClass() {
    return `s-spinner--${this.size}`;
  }

  get swapMode() {
    if (this.swap === true) {
      return "s-spinner--modeswap";
    }
  }
}
</script>

<style lang="less" scoped>
@import "./../styles/Imports";

.s-spinner {
  width: 100%;
  height: 100%;
  .padding();
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;
}

.s-spinner--tiny {
  height: 14px;
  width: 9px;
}

.s-spinner--small {
  height: 40px;
  width: 28px;
}

.s-spinner--large {
  height: 80px;
  width: 56px;
}

.s-spinner__bar {
  fill: @dark-2;
  opacity: 0.24;

  animation-name: breathe;
  animation-duration: 0.6s;
  animation-iteration-count: infinite;
  animation-direction: alternate;
  animation-delay: 0s;
  animation-timing-function: linear;

  &.s-spinner--modeswap {
    fill: @light-2;
  }

  &.middle {
    animation-delay: 0.4s;
  }
  &.last {
    animation-delay: 0.8s;
  }
}

.night,
.night-theme {
  .s-spinner__bar {
    fill: @light-2;

    &.s-spinner--modeswap {
      fill: @dark-2;
    }
  }
}

@keyframes breathe {
  from {
    opacity: 0.24;
    transform: scale3d(1, 1, 1) translate3d(0, 0, 0);
  }
  to {
    opacity: 0.08;
    transform: scale3d(1, 0.8, 1) translate3d(0, 4px, 0);
  }
}
</style>
