<template>
  <div class="content">
    <div class="content__inner">
      <BaseButton class="content__btn" :link="'#'"
        >Напомнить PIN-код</BaseButton
      >
      <BaseButton class="content__btn">отправить письмо</BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'secondary'"
        :iconClass="'icon-quest'"
        :isIcon="true"
      ></BaseButton>
      <BaseButton
        class="content__btn"
        :mode="'warning'"
        :iconClass="'icon-arrow'"
        ><template v-slot:icon-left
          ><span class="icon__left icon-arrow"></span></template
        ><template v-slot:icon-right
          ><span class="icon__right icon-exit"></span></template
        >отправить письмо</BaseButton
      >
      <BaseButton class="content__btn" :mode="'info'"
        ><template v-slot:icon-left
          ><span class="icon__left icon-arrow"></span></template
        >отправить письмо</BaseButton
      >
      <BaseButton class="content__btn" :mode="'danger'"
        ><template v-slot:icon-right
          ><span class="icon__right icon-arrow-right"></span></template
        >отправить письмо</BaseButton
      >
      <BaseButton class="content__btn" :mode="'action'"
        >отправить письмо</BaseButton
      >
      <BaseButton class="content__btn" disabled>отправить письмо</BaseButton>
    </div>
  </div>
</template>

<script></script>

<style lang="scss">
.content {
  @include _1024 {
    background-color: aquamarine;
  }
  &__inner {
    display: grid;
    grid-template-columns: max-content;
    justify-content: center;
    justify-items: center;
    margin: 0 auto;
    padding-top: 50px;
    text-align: center;
  }
  &__btn {
    margin-bottom: 10px;
  }
}
.icon {
  &__left {
    margin-right: 10px;
  }
  &__right {
    margin-left: 10px;
  }
}
</style>
