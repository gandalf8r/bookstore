<script setup>
defineProps({
  totalPrice: Number,
});

const emit = defineEmits(['openDrawer', 'freezeBody']);

const onCartOpen = () => {
  emit('openDrawer')
  emit('freezeBody')
}
</script>

<template>
  <heder class="flex flex-col lg:flex-row justify-between border-b border-slate-200 px-10 py-8">
    <router-link to="/">
      <div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-10"/>
        <div>
          <h2 class="text-xl font-bold uppercase">Book worm</h2>
          <p class="text-slate-500">Best books market</p>
        </div>
      </div>
    </router-link>

    <ul class="flex flex-col md:flex-row items-center gap-10 mt-4 lg:mt-0">
      <li @click="onCartOpen" class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
        <img src="/cart.svg" alt="Cart"/>
        <b>{{ totalPrice.toFixed(2)}}$</b>
      </li>

      <li class="flex gap-10">
        <router-link to="/favorites">
          <div class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
            <img src="/heart.svg" alt="Bookmark"/>
            <span>Bookmarks</span>
          </div>
        </router-link>

        <div class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/profile.svg" alt="Profile"/>
          <span>Profile</span>
        </div>
      </li>
    </ul>
  </heder>
</template>