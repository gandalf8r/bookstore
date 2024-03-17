<script setup>
import CartItem from '@/components/CartItem.vue'
import { inject } from 'vue'

const { cart, removeFromCart } = inject('cart')

</script>

<template>
  <div class="flex flex-col gap-4" v-auto-animate>
    <CartItem
      v-for="item in cart"
      :key="item"
      :title="item.title"
      :author="item.author"
      :price="item.price"
      :image-url="item.image"
      @on-click-remove="() => removeFromCart(item)" />
  </div>
</template>