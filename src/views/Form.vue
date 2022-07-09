<template>
  <div class="page">
    <div class="content">
      <form onsubmit="return postQuestion();" class="form">
        <h1 class="h-header-4 form__header">Add Questions here</h1>
        <div class="form__container">
          <label for="question" class="form__label">Question</label>
          <input
            type="text"
            name="question"
            class="form__input"
            v-model="question"
          />
          <label for="ans1" class="form__label">Answer 1</label>
          <input
            type="text"
            name="ans1"
            class="form__input"
            v-model="answers[0]"
          />
          <label for="ans2" class="form__label">Answer 2</label>
          <input
            type="text"
            name="ans2"
            class="form__input"
            v-model="answers[1]"
          />
          <label for="ans3" class="form__label">Answer 3</label>
          <input
            type="text"
            name="ans3"
            class="form__input"
            v-model="answers[2]"
          />
          <label for="corr_idx" class="form__label">Correct Index</label>
          <input
            type="number"
            min="0"
            max="2"
            name="corr_idx"
            class="form__input"
            v-model="corr_idx"
          />
          <button class="form__button" type="submit">Submit</button>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
export default {
  name: "Questions and Answers",
  data() {
    return {
      question: "",
      answers: [],
      corr_idx: 0,
    };
  },
  methods: {
    postQuestion() {
      (async () => {
        const rawResponse = await fetch("http://127.0.0.1:7777/questions", {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            question: this.question,
            answers: this.answers,
            corr_idx: this.corr_idx,
          }),
        });
        const content = await rawResponse.json();
        console.log(content);
      })();
    },
  },
};
</script>
<style lang="scss" scoped>
.page {
  height: 100vh;
  width: 100vw;
  box-sizing: border-box;
}
.content {
  box-sizing: border-box;
  padding: 100px;
  display: flex;
  width: 100%;
  justify-content: center;
}
.form {
  border-radius: 10px;
  width: 50vw;
  background-color: var(--color-white-1);
  box-sizing: border-box;
  padding: 50px;

  &__container {
    display: flex;
    flex-direction: column;
    height: 100%;
    widows: 100%;
  }
  &__input {
    width: 100%;
    font-size: var(--t-text-normal);
    color: var(--color-grey-2);
    padding: 16px 32px;
    box-sizing: border-box;
    border-radius: 4px;
    border: 1px solid var(--color-grey-4);
  }
  &__label {
    margin: 10px 0px;
    display: block;
    text-align: left;
    color: var(--color-grey-2);
  }
  &__button {
    margin: 30px;
    background-color: var(--color-brand-4);
    height: 50px;

    border-radius: 8px;
    border: none;

    color: var(--color-white-1);
    font-size: var(--text-size-1);
    font-weight: bold;

    transition: all 0.2s ease;
  }
  &__button:hover {
    box-shadow: inset 0 0 100px 100px rgba($color: #fff, $alpha: 0.2);
  }
  &__button:active {
    box-shadow: inset 0 0 100px 100px rgba($color: #000000, $alpha: 0.2);
  }
  &__header {
    margin-top: 0;
  }
}
</style>
