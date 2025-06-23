<script setup>
const props = defineProps({
  resultOpp: { type: Number, required: true },
  resultYou: { type: Number, required: true },
})
</script>

<template>
  <div class="counters">
    <div class="counter">{{ resultYou }}</div>
    <div class="counter">{{ resultOpp }}</div>
  </div>
</template>

<style scoped>
.counters {
  display: flex;
  justify-content: center;
  gap: 100px;
  width: 100%;
  font-family: 'Times New Roman', Times, serif;
  font-size: 50px;
}

.counter {
  min-width: 60px;
  text-align: center;
}
</style>
