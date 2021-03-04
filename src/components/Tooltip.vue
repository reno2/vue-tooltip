<template>
  <div
    class="tooltip"
    v-on:mouseleave="isShown = false"
    v-on:mouseover="isShown = true"
    :class="{ active: isShown }"
  >
    <div ref="tooltipTarget" class="tooltip_target">
      <slot name="target">
        <img class="tooltip_icon" src="../assets/info.png" />
      </slot>
    </div>

    <transition name="fade">
      <div
        ref="tooltipContainer"
        v-show="isShown"
        class="tooltip_container whiteBillet"
      >
        <slot></slot>
      </div>
    </transition>
  </div>
</template>
<script>
export default {
  props: {
    show: {
      type: Boolean,

      defautl: false,
    },
    transition: {
      type: String,
      default: "fade",
    },
  },
  data() {
    return {
      isShown: false,
      tooltipLeft: "",
      tooltipTop: "",
      defaultOffset: 20,
    };
  },
  methods: {
    calcPosition() {
      const {
        left: targetLeft,
        right: targetRight,
        top: targetTop,
        height: targetHeight,
        width: targetWidth,
        bottom: targetBottom,
      } = this.$refs.tooltipTarget.getBoundingClientRect();
      const {
        left: parentLeft,
        top: parentTop,
        right: parentRight,
        height: parentHeight,
        width: parentWidth,
        bottom: parentBottom,
      } = this.$el.getBoundingClientRect();
      const elementWidth = this.$refs.tooltipContainer.clientWidth;
      const elementHeight = this.$refs.tooltipContainer.clientHeight;
      const offsetByTarget =
        targetWidth > this.defaultOffset ? this.defaultOffset : targetWidth / 2;

      if (document.documentElement.clientWidth > targetRight + elementWidth) {
        // Если контейнер вмещается справа от таргета до края области просмотра,
        // то выставляем позицию справа от таргета с вычитом отступа объявленного в компоненте
        this.tooltipLeft =
          targetLeft - parentLeft + targetWidth - offsetByTarget;
      } else {
        this.tooltipLeft =
          parentRight - targetRight - elementWidth + targetWidth;
      }

      // Если высота видимой области меньше чем растояние до нижней точки таргета плюс высота контейнера,
      // то смещаем контейнер над таргетом
      if (window.innerHeight < targetBottom + elementHeight) {
        this.tooltipTop = targetTop - parentTop - elementHeight;
      } else {
        this.tooltipTop = targetTop - parentTop + targetHeight;
      }
    },
  },
  watch: {
    // Используем watch так как ничего не возвращаем
    isShown: function(newVal) {
      if (newVal) {
        this.$nextTick(() => {
          this.calcPosition();
          this.$refs.tooltipContainer.style.cssText = `left: ${this.tooltipLeft}px;top:${this.tooltipTop}px`;
        });
      }
    },
  },
};
</script>
<style>
.tooltip.active {
  z-index: 102;
}
.tooltip {
  position: relative;
  width: fit-content;
}
.tooltip.active .tooltip_container {
  background: #ffffff;
  box-shadow: 0px 4px 15px rgba(120, 160, 190, 0.3);
  padding: 24px;
  border-radius: 10px;
  z-index: 2000;
}
.tooltip_target {
  z-index: 1;
  cursor: pointer;
}
.tooltip_icon {
  fill: #82c831;
  width: 20px;
  height: 20px;
}
.tooltip_icon:hover {
  fill: #c1e499;
}
.tooltip_container {
  padding: 24px;
  z-index: 10;
  width: fit-content;
  position: absolute;
  top: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
