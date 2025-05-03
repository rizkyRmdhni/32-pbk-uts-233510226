<script setup>
import { ref, computed } from 'vue'

const items = ref([])
const newItem = ref('')
const filter = ref('all')

const addItem = () => {
  if (newItem.value !== '') {
    items.value.push({
      id: items.value.length + 1,
      text: newItem.value,
      completed: false
    })
    newItem.value = ''
  }
}

const toggle = (item) => {
  item.completed = !item.completed
}

const remove = (item) => {
  items.value = items.value.filter(i => i.id !== item.id)
}

const filteredItem = computed(() =>{
  if(filter.value === "completed"){
    return items.value.filter (item => item.completed)
  }else if(filter.value === "active"){
    return items.value.filter(item => !item.completed)
  }else{
    return items.value
  }
})

</script>

<template>
  <input type="text" v-model="newItem" @keyup.enter="addItem">
  <button @click="addItem">Tambahkan</button>
  <select v-model="filter">
    <option value="all">Semua</option>
    <option value="active">Aktif</option>
    <option value="completed">Selesai</option>
  </select>

  <ul>
    <li v-for="item in filteredItem" :key="item.id">
      <input type="checkbox" :checked="item.completed" @change="toggle(item)">
      {{ item.text }}
      <button @click="remove(item)">Hapus</button>
    </li>
  </ul>
</template>

<style scoped></style>
