<template>
  <div class="game container" id="app">
    <h1>Simon Says</h1>
    <div class="game__wrapper">
      <GameBtns
        class="game__btns"
        v-bind:gameBtnsDisabled="gameBtnsDisabled"
        v-bind:sounds="sounds"
        v-bind:playSound="soundOn"
        @check-btn="checkBtn"
      />
      <div class="game__panel">
        <p class="game__title">Round: {{round}}</p>
        <button v-on:click="startGame">Start</button>
        <p v-if="round == 0 && lastRound > 0">Sorry, you lost after {{lastRound}} rounds!</p>
        <p class="game__title">Game Options:</p>
        <GameOptions @change-delay="changeDelay" />
      </div>
    </div>
  </div>
</template>

<script>
import GameBtns from "./components/GameBtns.vue";
import GameOptions from "./components/GameOptions.vue";

const DELY_NEXT_ROUN_IN_MS = 500;
const DELY_ACTIVE_BTN_CLASS_IN_MS = 100;

let audioBlueBtn = new Audio(require("@/assets/media/1.mp3"));
let audioRedBtn = new Audio(require("@/assets/media/2.mp3"));
let audioYellowBtn = new Audio(require("@/assets/media/3.mp3"));
let audioGreenBtn = new Audio(require("@/assets/media/4.mp3"));

export default {
  name: "App",
  data() {
    return {
      round: 0,
      lastRound: 0,
      delayInMs: 1500,
      gameBtnsDisabled: true,
      btnsLine: [],
      clickCount: 0,
      soundOn: this.playSound,
      sounds: [audioBlueBtn, audioRedBtn, audioYellowBtn, audioGreenBtn]
    };
  },
  methods: {
    startGame() {
      this.round = 1;
      this.lastRound = 1;
      this.clickCount = 0;
      this.btnsLine = [];

      this.randomBtnAdd();
      this.playNeedLine();
    },
    randomBtnAdd() {
      let randomBtnIndex = this.getRandomInt(0, 4);

      this.btnsLine.push(randomBtnIndex);
    },
    playNeedLine() {
      let gameBtnsElements = document.querySelectorAll(".game-btn");

      for (let i = 0; i < this.btnsLine.length; i++) {
        setTimeout(() => {
          let randomBtnElement = gameBtnsElements[this.btnsLine[i]];
          let sound = this.sounds[this.btnsLine[i]];

          randomBtnElement.classList.add("game-btn--active");
          this.playSound(sound);

          setTimeout(() => {
            randomBtnElement.classList.remove("game-btn--active");
          }, DELY_ACTIVE_BTN_CLASS_IN_MS);

          if (this.btnsLine.length == ++i) {
            this.gameBtnsDisabled = false;
          }
        }, this.delayInMs * i);
      }
    },
    checkBtn(btnIndex) {
      if (this.btnsLine[this.clickCount] == btnIndex) {
        this.clickCount++;

        if (this.clickCount == this.round) {
          this.nextRound();
        }
      } else {
        this.gameOver();
      }
    },
    nextRound() {
      this.gameBtnsDisabled = true;
      this.clickCount = 0;
      this.round++;
      this.lastRound++;

      setTimeout(() => {
        this.randomBtnAdd();
        this.playNeedLine();
      }, DELY_NEXT_ROUN_IN_MS );
    },
    gameOver() {
      this.round = 0;
      this.gameBtnsDisabled = true;
    },
    changeDelay(time) {
      this.delayInMs = time;
    },
    playSound(audio) {
      if (!audio.ended) {
        audio.pause();
        audio.currentTime = 0.0;
      }
      audio.play();
    },
    getRandomInt(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    }
  },
  components: {
    GameBtns,
    GameOptions
  }
};
</script>

<style lang="scss" scoped>
h1 {
  margin-bottom: 60px;
  text-align: center;
  font-weight: 600;
  font-size: 38px;
}

p {
  font-size: 17px;
}

.game__wrapper {
  display: flex;
}

.game__btns {
  margin-right: 50px;
}

.game__title {
  margin-bottom: 5px;
  font-size: 28px;
  font-weight: 600;
}

button {
  transition: all 0.2s;
  min-width: 120px;
  padding: 5px 10px;
  margin-top: 15px;
  border: none;
  border-radius: 10px;
  font-size: 24px;
  font-weight: 500;
  background-color: $btn-color--main;

  &:hover {
    background-color: $btn-color--main-hover;
  }
}
</style>
