<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import CardList from '../components/CardList.vue'
/*Список добавленных в закладки кроссовки*/
const Favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://2581bcba99768b2b.mokky.dev/favorites?_relations=items'
    )

    Favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>

<template>
  <h2 class="text-3xl font-bold mb-8">Мои закладки</h2>

  <CardList :items="Favorites" is-favorites />
</template>
