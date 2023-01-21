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
    <span v-if="!iconClass">{{ isTimerActive ? timerBtnName : btnName }}</span>
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

<script setup>
import { ref, computed, onUnmounted, watch } from "vue";
const emits = defineEmits(["sendEmail"]);
const props = defineProps({
  btnName: {
    type: String,
    default: "",
  },
  timerBtnName: {
    type: String,
    default: "повторное письмо",
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
});
const currentTime = ref(30);
const timer = ref(null);
const isTimerActive = ref(false);

const btnClass = computed(() => {
  return [
    {
      "base-btn_disabled": props.disabled,
      "base-btn_secondary": props.mode === "secondary",
      "base-btn_warning": props.mode === "warning",
      "base-btn_info": props.mode === "info",
      "base-btn_danger": props.mode === "danger",
      "base-btn_action": props.mode === "action",
      "base-btn_icon": props.iconClass,
    },
  ];
});

onUnmounted(() => {
  stopTimer();
});
watch(currentTime, (time) => {
  if (time === -1) {
    stopTimer();
    isTimerActive.value = false;
  }
});

const click = () => {
  emits("sendEmail");
  if (props.isTimer) {
    timerOn();
  }
};
const timerOn = () => {
  if (isTimerActive.value === false) {
    currentTime.value = props.amountTime;
    isTimerActive.value = true;
    startTimer();
  }
};
const startTimer = () => {
  timer.value = setInterval(() => {
    currentTime.value--;
  }, 1000);
};
const stopTimer = () => {
  clearTimeout(timer.value);
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
