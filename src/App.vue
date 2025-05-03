<script setup>
import { ref, computed } from 'vue'

const items = ref([])
const newItem = ref('')
const filter = ref('all')

const addItem = () => {
  if (newItem.value.trim() !== '') {
    items.value.push({
      id: Date.now(),
      text: newItem.value,
      completed: false
    })
    newItem.value = ''
  }
}

const toggle = (item) => {
  item.completed == !item.completed
}

const remove = (item) => {
  items.value = items.value.filter(i => i.id !== item.id)
}

const filteredItem = computed(() => {
  if (filter.value === 'completed') {
    return items.value.filter(item => item.completed)
  } else if (filter.value === 'active') {
    return items.value.filter(item => !item.completed)
  } else {
    return items.value
  }
})
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-br from-indigo-100 via-purple-100 to-pink-100 flex items-center justify-center p-6 overflow-hidden">
    <div class="bg-white shadow-xl rounded-2xl w-full max-w-5xl flex overflow-hidden">

      <div class="w-1/3 bg-gradient-to-b from-purple-500 to-indigo-600 text-white p-6 flex flex-col justify-between">
        <div>
          <h2 class="text-2xl font-bold mb-4">To-Do App</h2>

          <input type="text" v-model="newItem" @keyup.enter="addItem" placeholder="Tugas baru..."
            class="w-full px-4 py-2 rounded-lg mb-3 text-gray-800 focus:outline-none focus:ring-2 focus:ring-white" />
          <button @click="addItem"
            class="w-full bg-white text-purple-700 font-semibold px-4 py-2 rounded-lg hover:bg-gray-100 transition">
            Tambah Tugas
          </button>
        </div>

        <div class="mt-8">
          <label class="block mb-2 font-medium">Filter</label>
          <select v-model="filter" class="w-full px-4 py-2 rounded-lg text-purple-800 focus:outline-none bg-white">
            <option value="all">Semua</option>
            <option value="active">Aktif</option>
            <option value="completed">Selesai</option>
          </select>
        </div>
      </div>

      <div class="w-2/3 p-6 overflow-y-auto h-[500px] space-y-4 bg-white">
        <h3 class="text-xl font-semibold text-gray-700 mb-4">Daftar Tugas</h3>
        <ul class="space-y-3">
          <li v-for="item in filteredItem" :key="item.id"
            class="flex justify-between items-center bg-gradient-to-r from-white to-purple-50 border border-purple-200 px-4 py-3 rounded-lg shadow-sm">
            <div class="flex items-center gap-3">
              <input type="checkbox" v-model="item.completed" @change="toggle(item)" class="accent-purple-600" />
              <span :class="{ 'line-through text-gray-400': item.completed }">{{ item.text }}</span>
            </div>
            <button @click="remove(item)" class="text-sm text-red-500 hover:underline">
              Hapus
            </button>
          </li>
        </ul>
      </div>

    </div>
  </div>
</template>

<style scoped></style>
