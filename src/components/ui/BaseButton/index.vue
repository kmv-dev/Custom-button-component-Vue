<template>
  <a v-if="link !== ''" class="base-btn__link" :href="link">
    <slot />
  </a>
  <button
    v-else
    class="base-btn"
    :class="[btnClass, { 'base-btn_disabled': isTimerActive }]"
    :type="type"
    @click="click()"
  >
    <span
      v-if="!isTimerActive && beforeIcon"
      class="base-btn__icon-left"
      :class="beforeIcon"
    ></span>
    <span v-if="!iconClass">{{
      isTimerActive ? "повторное письмо" : btnName
    }}</span>
    <span
      v-if="iconClass && !isTimerActive"
      class="base-btn__icon"
      :class="iconClass"
    ></span>
    <span
      v-if="!isTimerActive && afterIcon"
      class="base-btn__icon-right"
      :class="afterIcon"
    ></span>
    <div v-if="isTimerActive" class="base-btn__timer">{{ currentTime }}</div>
  </button>
</template>

<script>
export default {
  name: "BaseButton",
  props: {
    btnName: {
      type: String,
      default: "",
    },
    type: {
      type: String,
      default: "",
    },
    mode: {
      type: String,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    iconClass: {
      type: String,
      default: "",
    },
    link: {
      type: String,
      default: "",
    },
    isTimer: {
      type: Boolean,
      default: false,
    },
    beforeIcon: {
      type: String,
      default: "",
    },
    afterIcon: {
      type: String,
      default: "",
    },
    amountTime: {
      type: Number,
      default: 30,
    },
  },
  data() {
    return {
      currentTime: 30,
      timer: null,
      isTimerActive: false,
    };
  },
  unmounted() {
    this.stopTimer();
  },
  watch: {
    currentTime(time) {
      if (time === -1) {
        this.stopTimer();
        this.isTimerActive = false;
      }
    },
  },
  computed: {
    btnClass() {
      const { mode, disabled, iconClass } = this;
      return [
        {
          "base-btn_disabled": disabled,
          "base-btn_secondary": mode === "secondary",
          "base-btn_warning": mode === "warning",
          "base-btn_info": mode === "info",
          "base-btn_danger": mode === "danger",
          "base-btn_action": mode === "action",
          "base-btn_icon": iconClass,
        },
      ];
    },
  },
  methods: {
    click() {
      this.$emit("eventClick");
      if (this.isTimer) {
        this.timerOn();
      }
    },
    timerOn() {
      if (this.isTimerActive === false) {
        this.currentTime = this.amountTime;
        this.isTimerActive = true;
        this.startTimer();
      }
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.currentTime--;
      }, 1000);
    },
    stopTimer() {
      clearTimeout(this.timer);
    },
  },
};
</script>

<style lang="scss" scoped>
.base-btn {
  padding: 14px 46px;
  border-top-left-radius: 32px;
  border-bottom-left-radius: 36px;
  border-top-right-radius: 32px;
  border-bottom-right-radius: 26px;
  background: #702c7e;
  color: #ffffff;
  font-size: 16px;
  transition: 0.2s ease-in-out;
  text-transform: uppercase;
  -webkit-tap-highlight-color: transparent;
  transition: 0.2s ease-in-out;
  @include _640 {
    padding: 12px 26px;
    font-size: 14px;
  }
  &:hover {
    opacity: 0.8;
  }
  &__timer {
    margin-top: 2px;
    margin-left: 12px;
    padding: 1px 8px;
    background: #df3f3e;
    border-radius: 10px;
    color: #ffffff;
    font-size: 12px;
  }
  &__link {
    color: #c4296c;
    transition: 0.2s ease-in-out;
    &:hover {
      color: #767679;
    }
  }
  &_secondary {
    background: #c4296c;
  }
  &_warning {
    background: #f4ba46;
  }
  &_disabled {
    pointer-events: none;
    background: #efefef !important;
    color: #767679;
  }
  &_info {
    background: #0083b6;
  }
  &_danger {
    background: #df3f3e;
  }
  &_action {
    background: #ed732e;
  }
  &_icon {
    padding: 14px 30px;
    max-width: 60px;
    height: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    border-radius: 100%;
    @include _640 {
      max-width: 52px;
      height: 52px;
      font-size: 18px;
      padding: 14px 20px;
      margin: 0 auto 10px;
    }
  }
  &__icon-left {
    font-size: 24px;
    margin-right: 10px;
  }
  &__icon-right {
    font-size: 24px;
    margin-left: 10px;
  }
}
</style>
