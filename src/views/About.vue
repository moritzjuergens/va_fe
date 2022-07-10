<template>
  <div class="about">
    <h3 class="h-header-3">Highscore:</h3>
    <table class="table">
      <tr>
        <td class="table__header">Name</td>
        <td class="table__header">Score</td>
      </tr>
      <tr v-for="(x, index) in highscores" :key="index" class="table__row">
        <td class="table__item">{{ x.name }}</td>
        <td class="table__item">{{ x.score }}</td>
      </tr>
    </table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      highscores: [],
    };
  },
  mounted() {
    (async () => {
      const url = `https://sheltered-fjord-40724.herokuapp.com/highscores`;
      const rawResponse = await fetch(url, {
        method: "GET",
        headers: {
          Accept: "application/json",
        },
      });
      const content = await rawResponse.json();
      console.log(content);
      this.highscores = content;
      this.highscores = this.highscores.sort((a, b) => b.score - a.score);
    })();
  },
};
</script>
<style lang="scss" scoped>
.about {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.table {
  background: white;
  height: 20rem;
  width: 30rem;
  border-collapse: collapse;
  border: solid 1px var(--color-brand-5);

  box-sizing: content-box;
  &__header {
    border: solid 1px var(--color-brand-5);
    font-size: var(--header-size-4);
    font-weight: bold;
    margin: 20px;
  }
  &__row {
    border: solid 1px var(--color-brand-5);
  }
  &__item {
    border: solid 1px var(--color-brand-5);
  }
}
</style>
