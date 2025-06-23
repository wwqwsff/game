<template>
  <button class="bace-button" :class="[form, text, img, color]" @click="$emit('click')">
    <span v-if="form === 'rectangle'" class="button-text">
      {{ text === 'reset-game' ? 'RESET GAME' : text }}
    </span>
    <img v-else-if="img" :src="`/${img}.png`" :alt="img" class="button-icon" />
  </button>
</template>

<script setup>
const props = defineProps({
  form: {
    type: String,
    default: 'square',
  },
  text: {
    type: String,
    default: 'reset-game',
  },
  img: {
    type: String,
    default: 'rock',
  },
  color: {
    type: String,
    default: 'green',
  },
})
defineEmits(['click'])
// const messageRes = ref('RESULT!')
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
}
.rectangle {
  width: 360px;
  height: 72px;
}
.button-text {
  text-transform: uppercase;
}
.button-icon {
  max-width: 80%;
  max-height: 80%;
  object-fit: contain;
}
.green {
  background-color: #6b8e23;
}
.grey {
  background-color: #808080;
}
.pink {
  background-color: #db7093;
}
</style>
