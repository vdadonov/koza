<script>
  const formData = {
    minLimit: 10,
    maxLimit: 20,
    text: '№ 0#-РПП/ЦМ/2019 от',
  };

  let generatorData = [];

  function generateData() {
    if (formData.minLimit && formData.maxLimit && formData.maxLimit > formData.minLimit) {
      generatorData = [];
      let i = Number(formData.minLimit, 10);
      while (i <= formData.maxLimit) {
        generatorData = [...generatorData, formData.text.replace('#', i)];
        i += 1;
      }
    }
  };
</script>

<style lang="scss">
  .ui-generator-form {
    display: flex;
    flex-direction: column;

    & div {
      &:not(:first-child) {
        margin-top: 10px;
      }
    }

    & .ui-generator-limit {
      display: flex;
      flex-direction: row;
      justify-content: space-between;

      & input {
        max-width: 45%;
      }
    }

    & .ui-generator-text {
      display: flex;

      & input {
        width: 100%;
      }
    }

    & .ui-generator-button {
      display: flex;

      & button {
        width: 100%;
      }
    }
  }

  .ui-generator-output {
    width: 100%;
    margin-top: 15px;

    & p {
      margin: 0px
    }
  }
</style>

<div>
  <form on:submit|preventDefault={generateData} class="ui-generator-form">
    <div class="ui-generator-limit">
      <input bind:value={formData.minLimit} placeholder="цифра, от" type="text" />
      <input bind:value={formData.maxLimit} placeholder="цифра, до" type="text" />
    </div>

    <div class="ui-generator-text">
      <input bind:value={formData.text} placeholder="текст, изменяемые цифры обвести ##" type="text" />
    </div>

    <div class="ui-generator-button">
      <button type="submit">генерировать</button>
    </div>
  </form>

  <div class="ui-generator-output">
    {#each generatorData as item}
      <p>{item}</p>
    {/each}
  </div>
</div>