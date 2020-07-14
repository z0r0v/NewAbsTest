<template>
  <h2 class="cong">{{text}}</h2>
</template>

<script>
    export default {
        name: "cong",
        data() {
            return {
                text: 'Поздравляем!',
            }
        }
    }
</script>

<style lang="scss">
  @import '../../varible.scss';
  .cong {
    margin-top: 89px;
    margin-bottom: 52px;

    @include textLine(30px, 35px, center,  $main-color-white);
    font-weight: bold;
    text-transform: uppercase;
  }

</style>
