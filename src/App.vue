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
</script>

<template>
  <input type="text" v-model="newItem" @keyup.enter="addItem">
  <button @click="addItem">Tambahkan</button>
</template>

<style scoped>

</style>
