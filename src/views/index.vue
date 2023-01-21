<template>
  <div class="content">
    <div class="content__inner">
      <BaseButton class="content__btn" :link="'#'"
        >Напомнить PIN-код</BaseButton
      >
      <BaseButton
        class="content__btn"
        :btnName="'кнопка с таймером'"
        :isTimer="true"
        :amountTime="100"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'secondary'"
        :iconClass="'icon-quest'"
        @eventClick="clickBtn"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'warning'"
        :beforeIcon="'icon-arrow'"
        :afterIcon="'icon-exit'"
        :btnName="'отправить письмо'"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'info'"
        :btnName="'кнопка с таймером'"
        :beforeIcon="'icon-vk'"
        :isTimer="true"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'danger'"
        :btnName="'отправить письмо'"
        :afterIcon="'icon-google'"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'action'"
        :btnName="'отправить письмо'"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        disabled
        :btnName="'отправить письмо'"
      ></BaseButton>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    clickBtn() {
      console.log("кликнули");
    },
  },
};
</script>

<style lang="scss">
.content {
  &__inner {
    display: grid;
    grid-template-columns: max-content;
    justify-content: center;
    justify-items: center;
    margin: 0 auto;
    padding-top: 50px;
    text-align: center;
    @include _640 {
      display: flex;
      flex-direction: column;
      padding: 50px 20px;
    }
  }
  &__btn {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
  }
}
</style>
