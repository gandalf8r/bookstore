<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import CardList from '@/components/CardList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(`https://9a9662826ecf7816.mokky.dev/favorites?_relations=books`)

    favorites.value = data.map(obj => obj.book)
    console.log(favorites.value)
  } catch (err) {
    console.log(err)
  }
})
</script>

<template>
  <h2 class="text-3xl font-bold mb-8">Bookmarks</h2>

  <CardList :items="favorites" is-favorites />
</template>

<style scoped>

</style>