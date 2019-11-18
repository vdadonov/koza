<script>
  import Generator from './components/Generator.svelte';
</script>

<style lang="scss">
  @import './assets/scss/_vars';
	.container {
    width: 1280px;

    @media only screen and (max-width: 410px) {
      width: 100% !important;
    }
    & .ui-generator {
      display: flex;
      justify-content: center;
      margin-top: 50px;

      & .ui-generator-wrap {
        width: 400px;
      }
    }
  }
</style>

<div class="container">
  <div class="ui-generator">
    <div class="ui-generator-wrap">
      <Generator />
    </div>
  </div>
</div>
