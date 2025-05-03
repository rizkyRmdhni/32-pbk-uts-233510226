<script setup>
import { ref } from 'vue'

const items = ref([])
const newItem = ref('')

const addItem = () => {
  if(newItem.value !== ''){
    items.value.push({
      id: items.value.length + 1,
      text: newItem.value,
      completed: false
    })
    newItem.value = ''
    console.log(items.value)
  }
}

const toggle = (item) => {
  item.completed = !item.completed
  console.log(item)
}

</script>

<template>
  <input type="text" v-model="newItem" @keyup.enter="addItem">
  <button @click="addItem">Tambahkan</button>

  <ul>
    <li v-for="item in items" :key="item.id">
      <input type="checkbox" :checked="item.completed" @change="toggle(item)">
      {{ item.text }}
    </li>
  </ul>
</template>

<style scoped>

</style>
