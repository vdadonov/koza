<script>
  const formData = {
    minLimit: 10,
    maxLimit: 20,
    text: '№ 0#',
  };

  let copyState = false;

  let generatorData = [];

  const generateData = () => {
    if (formData.minLimit && formData.maxLimit && Number(formData.maxLimit, 10) > Number(formData.minLimit, 10)) {
      generatorData = [];
      let i = Number(formData.minLimit, 10);
      while (i <= formData.maxLimit) {
        generatorData = [...generatorData, formData.text.replace('#', i)];
        i += 1;
      }
    }
  };

  function copyData() {
    const el = document.createElement('textarea');
    el.value = generatorData.join('\n');
    document.body.appendChild(el);
    el.select();

    try {
      document.execCommand('copy');

    }
    catch (error) {
      alert('Ошибка копирования, придется копировать вручную');
    }

    document.body.removeChild(el);

  };
</script>

<style lang="scss">

  .wrap {
    & .ui-generator-form {
      width: 100%;
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

        @media only screen and (max-width: 410px) {
          flex-direction: column !important;
        }

        & .ui-generator-limit-input {
          max-width: 45%;

          @media only screen and (max-width: 410px) {
            max-width: 100% !important;
          }
        }

        & :nth-child(2) {
          @media only screen and (max-width: 410px) {
            margin-top: 10px;
          }
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

    & .ui-generator-output {
      margin-top: 15px;
      & .ui-generator-output-copy {
        display: flex;
        justify-content: space-between;

        & .ui-generator-output-copy-title {
          font-size: 20px;
        }

        & .ui-generator-output-copy-wrap {
          display: flex;
          align-items: center;
          // background: #98c75a;
          border-radius: 4px;
          padding: 5px;

          & div {
            font-size: 12px;
            color: #fff;
          }

          & .ui-generator-output-copy-image {
            width: 16px;
            cursor: pointer;
            margin-left: 5px;
          }
        }
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

<div class="wrap">
  <form on:submit|preventDefault={generateData} class="ui-generator-form">
    <div class="ui-generator-limit">
      <input class="ui-generator-limit-input" bind:value={formData.minLimit} placeholder="цифра, от" type="text" />
      <input bind:value={formData.maxLimit} placeholder="цифра, до" type="text" />
    </div>

    <div class="ui-generator-text">
      <input new-password bind:value={formData.text} placeholder="текст, изменяемые цифры обвести ##" type="text" />
    </div>

    <div class="ui-generator-button">
      <button type="submit">генерировать</button>
    </div>
  </form>

  {#if generatorData.length > 0}
    <div class="ui-generator-output">
      <div class="ui-generator-output-copy" on:click="{copyData}">
        <div class="ui-generator-output-copy-title">Сгерерированные данные</div>

        {#if copyState}
          <div class="ui-generator-output-copy-wrap active">
            <div>скопировано</div>
            <img class="ui-generator-output-copy-image" src="./copy-content.svg"/>
          </div>
        {:else}
          <div class="ui-generator-output-copy-wrap">
            <img class="ui-generator-output-copy-image" src="./copy-content.svg"/>
          </div>
        {/if}


      </div>

      <div id="ui-generator-output-data">
        {#each generatorData as item}
          <p>{item}</p>
        {/each}
      </div>
    </div>
  {/if}
</div>