<template>
  <div>
    <label for="easy">
      <input
        type="radio"
        id="easy"
        name="difficulty"
        checked
        v-on:change="$emit('change-delay', difficulty.easy)"
      />
      Easy
    </label>
    <label for="normal">
      <input
        type="radio"
        id="normal"
        name="difficulty"
        v-on:change="$emit('change-delay', difficulty.normal)"
      />
      Normal
    </label>
    <label for="hard">
      <input
        type="radio"
        id="hard"
        name="difficulty"
        v-on:change="$emit('change-delay', difficulty.hard)"
      />
      Hard
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      difficulty: {
        easy: 1500,
        normal: 1000,
        hard: 400
      }
    };
  }
};
</script>

<style scoped lang="scss">
label {
  display: block;
  margin-bottom: 5px;
  font-size: 18px;
}
input {
  margin-right: 7px;
}
</style>