<template>
  <div>
    <ul>
      <li>
        <button
          class="game-btn game-btn--blue"
          v-on:click="playSound(sounds[0]), $emit('check-btn', 0)"
          v-bind:disabled="gameBtnsDisabled"
        ></button>
      </li>
      <li>
        <button
          class="game-btn game-btn--red"
          v-on:click="playSound(sounds[1]), $emit('check-btn', 1)"
          v-bind:disabled="gameBtnsDisabled"
        ></button>
      </li>
      <li>
        <button
          class="game-btn game-btn--yellow"
          v-on:click="playSound(sounds[2]), $emit('check-btn', 2)"
          v-bind:disabled="gameBtnsDisabled"
        ></button>
      </li>
      <li>
        <button
          class="game-btn game-btn--green"
          v-on:click="playSound(sounds[3]), $emit('check-btn', 3)"
          v-bind:disabled="gameBtnsDisabled"
        ></button>
      </li>
    </ul>
  </div>
</template>

<script>

export default {
  props: {
    gameBtnsDisabled: Boolean,
    sounds: Array,
    playSound: Function
  },
};
</script>

<style scoped lang="scss">
ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  width: 302px;
  height: 295px;
  padding: 0;
  padding-bottom: 5px;
  margin: 0;
  border-radius: 50%;
  box-shadow: 2px 1px 12px #aaa;
}

li {
  flex-basis: 49%;
  height: 145px;

  &:nth-of-type(1) button {
    border-top-left-radius: 100%;
  }

  &:nth-of-type(1) button:hover {
    border-left: 2px solid #000;
    border-top: 2px solid #000;
  }

  &:nth-of-type(2) button {
    border-top-right-radius: 100%;
  }

  &:nth-of-type(2) button:hover {
    border-right: 2px solid #000;
    border-top: 2px solid #000;
  }

  &:nth-of-type(3) button {
    border-bottom-left-radius: 100%;
  }

  &:nth-of-type(3) button:hover {
    border-left: 2px solid #000;
    border-bottom: 2px solid #000;
  }

  &:nth-of-type(4) button {
    border-bottom-right-radius: 100%;
  }

  &:nth-of-type(4) button:hover {
    border-right: 2px solid #000;
    border-bottom: 2px solid #000;
  }
}

.game-btn {
  width: 100%;
  height: 100%;
  border: none;
  opacity: 0.6;

  &--blue {
    background-color: $blue-btn;
  }

  &--red {
    background-color: $red-btn;
  }

  &--yellow {
    background-color: $yellow-btn;
  }

  &--green {
    background-color: $green-btn;
  }

  &--active,
  &:active {
    opacity: 1;
  }

  &:focus {
    outline: none;
  }
}
</style>
