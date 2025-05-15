<script setup lang="ts">
import { ref, computed, watch } from 'vue'
/* import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue' */
//const counter = ref(0)
const title = ref('Список заметок')
const placeh = ref('Введите название заметки')
const inputValue = ref('')

const notes = ref(['Заметка 1', 'Заметка 2'])
const addNewNote = () => {
  if (inputValue.value !== '') {
    notes.value.push(inputValue.value)
    inputValue.value = ''
  }
}
const removeNote = (idx: number) => {
  notes.value.splice(idx, 1)
}
const toUpperCase = (item: string) => {
  return item.toUpperCase()
}

const doubleCount = computed(() => {
  return notes.value.length * 2
})

watch(inputValue, (newValue) => {
  if (newValue.length > 10) {
    inputValue.value = newValue.slice(0, 10) // Обрезаем до 10 символов
  }
})
/* const inputKey = (event: KeyboardEvent) => {
  if (event.key === 'Enter') {
    addNewNote()
  }
} */
/* const increment = () => counter.value++
const decrement = () => counter.value-- */
</script>

<template>
  <header>
    <div class="container" id="app">
      <div class="card">
        <h1 :style="{ color: inputValue.length < 5 ? 'red' : 'blue' }">
          {{ title
          }}<!-- : {{ counter }} -->
        </h1>
        <!--   <div>
          <button class="btn primary" v-on:click="counter++">+</button>
          <button class="btn danger" v-on:click="counter--">-</button>
        </div> -->
        <div class="form-control">
          <input
            type="text"
            :placeholder="placeh"
            v-model="inputValue"
            @keypress.enter="addNewNote"
          />
        </div>
        <!-- <h2>inputValue: {{ inputValue }}</h2> -->
        <button class="btn" v-on:click="addNewNote">добавить</button>
        <hr />
        <ul class="list" v-if="notes.length !== 0">
          <li class="list-item" v-for="(myNote, idx) in notes">
            <span :class="myNote.length > 5 ? 'primery' : 'bold'"
              >({{ idx + 1 }}){{ toUpperCase(myNote) }}</span
            >
            <button class="btn danger" v-on:click="removeNote(idx)">удалить</button>
          </li>
          <hr />
          <li>
            <strong>Общее количество: {{ notes.length }}</strong
            >| Удвоеное: {{ doubleCount }}
          </li>
        </ul>
        <div v-else-if="notes.length === 0">Добавьте заметки</div>
      </div>
    </div>
  </header>
  <!-- 
  <RouterView /> -->
</template>

<style scoped>
/* Основные стили контейнера */
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

/* Карточка с заметками */
.card {
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 25px;
  margin-top: 20px;
}

/* Заголовок */
h1 {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 20px;
  font-size: 28px;
}

/* Форма ввода */
.form-control {
  margin-bottom: 15px;
}

/* Поле ввода */
input[type='text'] {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  box-sizing: border-box;
  transition: border-color 0.3s;
}

input[type='text']:focus {
  border-color: #42b983;
  outline: none;
  box-shadow: 0 0 0 2px rgba(66, 185, 131, 0.2);
}

/* Кнопки */
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
  transition: all 0.3s;
  margin-right: 10px;
}

/* Основная кнопка добавления */
.btn {
  background-color: #42b983;
  color: white;
}

.btn:hover {
  background-color: #3aa876;
}

/* Опасная кнопка (удаление) */
.btn.danger {
  background-color: #ff4757;
  color: white;
  padding: 5px 10px;
  font-size: 14px;
}

.btn.danger:hover {
  background-color: #ff6b81;
}

/* Разделительная линия */
hr {
  border: 0;
  height: 1px;
  background-color: #eee;
  margin: 20px 0;
}

/* Список заметок */
.list {
  list-style: none;
  padding: 0;
  margin: 0;
}

/* Элемент списка */
.list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 15px;
  background-color: #f9f9f9;
  border-radius: 5px;
  margin-bottom: 10px;
  transition: background-color 0.3s;
}

.list-item:hover {
  background-color: #f0f0f0;
}

/* Нумерация заметок */
.list-item::before {
  content: counter(item);
  counter-increment: item;
  margin-right: 10px;
  color: #666;
}

/* Адаптивность для мобильных устройств */
@media (max-width: 600px) {
  .container {
    padding: 10px;
  }

  .card {
    padding: 15px;
  }

  .list-item {
    flex-direction: column;
    align-items: flex-start;
  }

  .btn.danger {
    margin-top: 8px;
    align-self: flex-end;
  }
}
</style>
