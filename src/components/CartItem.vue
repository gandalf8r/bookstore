<script setup>
const emit = defineEmits(['onClickRemove']);

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  author: String,
  price: Number
})
</script>

<template>
  <div class="flex items-center border border-slate-200 p-4 rounded-xl gap-4">
    <img class="w-16 h-24" :src="imageUrl" alt="Book">
    <div class="flex flex-col flex-1">
      <p>{{ title }}</p>
      <p class="opacity-50 text-xs">{{ author }}</p>
      <div class="flex justify-between mt-2">
        <b class="flex-1">{{ price }}$</b>
        <img @click="emit('onClickRemove')" class="opacity-40 hover:opacity-100 cursor-pointer transition" src="/close.svg" alt="Close">
      </div>
    </div>
  </div>
</template>