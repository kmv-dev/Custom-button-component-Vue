<template>
  <button class="base-btn" :class="btnClass" :type="type">
    <span v-if="isIcon" class="base-btn__icon" :class="iconClass" />
    <slot />
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
    isIcon: {
      type: Boolean,
      default: false,
    },
    iconClass: {
      type: String,
      default: "",
    },
  },
  computed: {
    btnClass() {
      const { mode, disabled } = this;
      return [
        {
          "base-btn_disabled": disabled,
          "base-btn_logout": mode === "logout",
        },
      ];
    },
  },
};
</script>

<style lang="scss" scoped>
.base-btn {
  padding: 14px 46px;
  border-top-left-radius: 34px;
  border-bottom-left-radius: 38px;
  border-top-right-radius: 38px;
  border-bottom-right-radius: 34px;
  background: #702c7e;
  color: #ffffff;
  font-size: 18px;
  transition: 0.2s ease-in-out;
  text-transform: uppercase;
  &:hover {
    box-shadow: none;
  }
  &__icon {
    margin-right: 5px;
  }
  &_disabled {
    pointer-events: none;
    opacity: 0.5;
  }
  &_logout {
    background: #f2f0f2;
    color: #5787a4;
  }
}
</style>
