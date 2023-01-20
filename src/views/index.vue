<template>
  <div class="content">
    <div class="content__inner">
      <BaseButton>отправить письмо</BaseButton>
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
    margin: 0 auto;
    padding-top: 50px;
    text-align: center;
  }
}
</style>
