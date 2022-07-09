<template>
  <div class="home">
    <div class="content">
      <div id="form" class="jumbo">
        <div class="jumbo__content">
          <h3 class="h-header-3 jumbo__content__question">Enter your Name</h3>
          <form @submit="event.preventDefault()" class="form">
            <label for="name" class="form__label">Name: </label>
            <input
              type="text"
              name="name"
              class="form__input"
              v-model="player"
            />
            <button class="form__button" type="button" @click="startGame">
              Submit
            </button>
          </form>
        </div>
      </div>

      <div id="quiz" class="jumbo">
        <div class="jumbo__header">
          <div class="jumbo__header__item">
            Question: {{ cnt + 1 }} / {{ questions.length }}
          </div>
          <div class="jumbo__header__item">Score: {{ numCorrect }}</div>
          <div class="jumbo__header__item">Time: {{ timerCount }}</div>
        </div>
        <div class="jumbo__content">
          <h3 class="h-header-4 jumbo__content__question">
            {{ currentQuestion.question }}
          </h3>
          <div class="jumbo__content__answers">
            <div
              v-for="(answer, index) in currentQuestion.answers"
              :key="index"
              :id="index"
              @click="selectAnswer(index)"
              class="jumbo__content__answers__item"
              :class="answerClass(index)"
            >
              {{ answer }}
            </div>
            <button
              class="jumbo__content__button"
              id="submit"
              @click="submitAnswer"
            >
              Submit Answer
            </button>
            <button class="jumbo__content__button" id="next" @click="next">
              Next Question
            </button>
            <button class="jumbo__content__button" id="finish" @click="finish">
              Finish Quiz
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: "Home",
  components: {},
  data() {
    return {
      player: "",
      questions: [],
      numCorrect: 0,
      game: {},
      gameInfo: [],
      gameID: "",
      currentQuestion: [],
      cnt: 0,
      answer_given: null,
      answered: false,
      corr_idx: null,
      timerCount: 20,
      timerEnabled: false,
    };
  },
  watch: {
    timerEnabled(value) {
      if (value) {
        setTimeout(() => {
          this.timerCount--;
        }, 1000);
      }
    },

    timerCount: {
      handler(value) {
        if (value > 0 && this.timerEnabled) {
          setTimeout(() => {
            this.timerCount--;
          }, 1000);
        } else if (value <= 0 && this.timerEnabled) {
          this.answer_given = 5;
          this.submitAnswer();
          this.next();
        }
      },
      immediate: true, // This ensures the watcher is triggered upon creation
    },
  },
  // mounted() {
  //   fetch("http://127.0.0.1:7777/questions", {
  //     method: "get",
  //   })
  //     .then((response) => {
  //       return response.json();
  //     })
  //     .then((jsonData) => {
  //       this.questions = jsonData;
  //       console.log(jsonData);
  //     });
  // },
  methods: {
    startGame() {
      (async () => {
        const url = `https://sheltered-fjord-40724.herokuapp.com/start/${this.player}/10`;
        const rawResponse = await fetch(url, {
          method: "GET",
          headers: {
            Accept: "application/json",
          },
        });
        const content = await rawResponse.json();
        console.log(content);
        this.game = content;
        this.gameID = this.game.game_id;
        this.gameInfo = this.game.game_info;
        this.questions = this.gameInfo.questions;
        this.currentQuestion = this.questions[0];
      })();
      this.timerEnabled = true;
      document.getElementById("form").style.display = "none";
      document.getElementById("quiz").style.display = "block";
    },
    selectAnswer(index) {
      //console.log(index);
      this.answer_given = index;
      //this.answered = true;
    },
    answerClass(index) {
      let answerClass = "";
      if (!this.answered && this.answer_given === index) {
        answerClass = "selected";
      }
      return answerClass;
    },
    next() {
      this.timerEnabled = true;
      if (this.cnt == this.questions.length - 1) {
        document.getElementById("next").style.display = "none";
        document.getElementById("submit").style.display = "none";
        document.getElementById("finish").style.display = "block";
        return;
      }
      this.cnt++;
      this.currentQuestion = this.questions[this.cnt];
      document
        .getElementById(this.answer_given)
        .classList.remove("correct", "wrong");
      this.answer_given = null;
      document.getElementById("next").style.display = "none";
      document.getElementById("submit").style.display = "block";
    },
    submitAnswer() {
      this.timerEnabled = false;

      (async () => {
        const url = `https://sheltered-fjord-40724.herokuapp.com/answer`;
        //const url = "http://127.0.0.1:5000/answer";
        const rawResponse = await fetch(url, {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            game_id: this.gameID,
            question_id: this.currentQuestion.id,
            answer_given: this.answer_given,
          }),
        });
        const content = await rawResponse.json();
        console.log(content);
        if (content.answer) {
          this.numCorrect++;
          document.getElementById(this.answer_given).classList.add("correct");
        } else {
          this.numCorrect--;
          document.getElementById(this.answer_given).classList.add("wrong");
        }
        if (this.cnt == this.questions.length - 1) {
          this.next();
          return;
        }
        this.timerCount = 20;
        document.getElementById("submit").style.display = "none";
        document.getElementById("next").style.display = "block";
      })();
    },
    finish() {
      (async () => {
        const url = `https://sheltered-fjord-40724.herokuapp.com/finish`;
        const rawResponse = await fetch(url, {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json",
          },
          body: JSON.stringify({
            game_id: this.gameID,
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
.home {
  height: 100vh;
  width: 100vw;
}
.content {
  box-sizing: border-box;
  padding: 100px;
  display: flex;
  height: 100%;
  width: 100%;

  justify-content: center;
}
.jumbo {
  height: 35rem;
  width: 70rem;
  box-sizing: border-box;
  padding: 20px;
  background-color: var(--color-white-1);
  display: flex;
  flex-direction: column;
  border-radius: 10px;

  &__header {
    height: 15%;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    &__item {
      left: 0;
    }
  }

  &__content {
    display: flex;
    place-items: center;
    flex-direction: column;
    &__question {
      margin: 0;
    }
    &__answers {
      height: 20rem;
      width: 60%;
      margin: 50px;
      display: grid;
      grid-template-rows: auto auto auto auto;
      place-items: center;

      &__item {
        height: 100%;
        width: 100%;
        cursor: pointer;
        display: flex;
        align-items: center;
        place-content: center;
        border: 1px solid var(--color-grey-4);
      }
    }
    &__button {
      margin: 30px;
      background-color: var(--color-brand-4);
      height: 50px;
      width: 20rem;

      border-radius: 8px;
      border: none;

      color: var(--color-white-1);
      font-size: var(--text-size-1);
      font-weight: bold;

      transition: all 0.2s ease;
    }
  }
}
#quiz {
  display: none;
}
.form {
  border-radius: 10px;
  width: 50vw;
  background-color: var(--color-white-1);
  box-sizing: border-box;
  padding: 50px;
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
    width: 20rem;

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
}
.selected {
  background-color: lightskyblue;
}
.correct {
  background-color: greenyellow;
}
.wrong {
  background-color: indianred;
}
#next {
  display: none;
}
#finish {
  display: none;
}
</style>
