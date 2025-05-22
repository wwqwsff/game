<template>
  <button class="bace-button" :class="[form, text, img]" @click="$emit('click')">
    <span v-if="form === 'rectangle'" class="button-text">
      {{ text === 'reset-game' ? 'RESET GAME' : text }}
      <!-- надо добавить стилей надписи -->
    </span>
    <img v-else-if="img" :src="`/${img}.png`" :alt="img" class="button-icon" />
  </button>
</template>
<script>
export default {
  props: {
    form: {
      type: String,
      default: 'square', //rectangle
    },

    text: {
      type: String,
      default: 'reset-game', //nottext
    },
    img: {
      type: String,
      default: 'rock', //rock paper scissors
    },
  },
}
</script>
<style scoped>
.bace-button {
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  border: none;
  font-weight: bold;
}
.square {
  width: 150px;
  height: 150px;
  background-color: #6b8e23;
}
.rectangle {
  width: 360px;
  height: 72px;
  background-color: #db7093;
}
.button-text {
  text-transform: uppercase;
}
.button-icon {
  max-width: 80%;
  max-height: 80%;
  object-fit: contain;
}
</style>
