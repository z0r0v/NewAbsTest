<template>
  <h2 class="get-euros"><span>{{getText}}</span><span>{{getNextText}}</span></h2>
</template>

<script>
    export default {
        name: "GetEurosComponent",
        data() {
            return {
                getText: '"Получать 1000 евро',
                getNextText: 'каждую неделю!"',
            }
        }
    }
</script>


<style lang="scss">
  @import '../varible.scss';
  .get-euros {
    margin-top: 33px;
    margin-bottom: 87px;
    @include textLine(23px, 28px, center, $main-color-white);
    font-weight: bold;
    text-transform: uppercase;
    span {
      display: block;
    }
  }

</style>
