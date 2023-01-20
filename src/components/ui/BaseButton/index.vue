<template>
  <a v-if="link !== ''" class="base-btn__link" :href="link">
    <slot />
  </a>
  <button v-else class="base-btn" :class="btnClass" :type="type">
    <slot name="icon-left"></slot>
    <slot v-if="!isIcon" />
    <span
      v-if="isIcon && iconClass"
      class="base-btn__icon"
      :class="iconClass"
    ></span>
    <slot name="icon-right"></slot>
  </button>
</template>

<script>
export default {
  name: "BaseButton",
  props: {
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
    iconSide: {
      type: String,
      default: "",
    },
    isIcon: {
      type: Boolean,
      default: false,
    },
    link: {
      type: String,
      default: "",
    },
  },
  computed: {
    btnClass() {
      const { mode, disabled, isIcon } = this;
      return [
        {
          "base-btn_disabled": disabled,
          "base-btn_secondary": mode === "secondary",
          "base-btn_warning": mode === "warning",
          "base-btn_info": mode === "info",
          "base-btn_danger": mode === "danger",
          "base-btn_action": mode === "action",
          "base-btn_icon": isIcon,
        },
      ];
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
    background: #efefef;
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
  }
}
</style>
