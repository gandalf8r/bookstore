<script setup>
const props = defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  author: String,
  price: Number,
  isFavorite: Boolean,
  isAdded: Boolean,
  onClickFavorite: Function,
  onClickAdd: Function
})

const visibleFavoriteButton = Boolean(props.onClickAdd)
</script>

<template>
  <div class="relative flex flex-col justify-between bg-white border border-slate-100 rounded-xl p-6 cursor-pointer hover:-translate-y-2 hover:shadow-xl transition">
    <img
      v-if="visibleFavoriteButton"
      :src="!isFavorite ? '/like-1.svg' : '/like-2.svg'"
      alt="Like 1"
      class="absolute top-2 left-2"
      @click="onClickFavorite" />
    <div class="flex items-center justify-between gap-2">
      <div class="flex flex-col">
        <p class="mt-2">{{ title }}</p>
        <p class="opacity-50 text-xs">{{ author }}</p>
      </div>
      <img class="w-3/4 h-full md:w-32 md:h-40" :src="imageUrl" alt="Sneaker" />
    </div>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Price:</span>
        <b>{{ price }}$</b>
      </div>

      <img v-if="visibleFavoriteButton" @click="onClickAdd" :src="!isAdded ? '/plus.svg' : '/checked.svg'" alt="Plus" />
    </div>
  </div>
</template>