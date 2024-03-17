<script setup>
import { ref, provide, watch, computed } from 'vue'

import Header from '@/components/Header.vue'
import Drawer from '@/components/Drawer.vue'

/* Cart */
const cart = ref([])
const drawerOpen = ref(false)

const totalPrice = computed(() => cart.value.reduce((acc, item) => acc + item.price, 0))
const vatPrice = computed(() => (totalPrice.value * 0.05).toFixed(2))

const openDrawer = () => {
  drawerOpen.value = true
}

const closeDrawer = () => {
  drawerOpen.value = false
}

const addToCart = (item) => {
  cart.value.push(item)
  item.isAdded = true
}

const removeFromCart = (item) => {
  cart.value.splice(cart.value.indexOf(item), 1)
  item.isAdded = false
}

watch(cart, () => {
  localStorage.setItem('cart', JSON.stringify(cart.value))
}, { deep: true })

const freezeBody = () => {
  const body = document.querySelector('body');
  body.classList.add('freeze')
}

const freeBody = () => {
  const body = document.querySelector('body');
  body.classList.remove('freeze')
}

provide('cart', {
  cart,
  openDrawer,
  closeDrawer,
  addToCart,
  removeFromCart,
  freezeBody,
  freeBody,
})

/* Cart end */
</script>

<template>
  <Drawer
    v-if="drawerOpen"
    :total-price="totalPrice"
    :vat-price="vatPrice" />
  <div class="bg-white w-11/12 md:w-4/5 m-auto rounded-xl shadow-xl mt-14">
    <Header :total-price="totalPrice" @open-drawer="openDrawer" @freeze-body="freezeBody" />

    <div class="p-10">
      <router-view></router-view>
    </div>
  </div>
</template>

<style>

</style>
