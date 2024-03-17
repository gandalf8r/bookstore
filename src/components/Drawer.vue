<script setup>
import DrawerHead from '@/components/DrawerHead.vue'
import CartItemList from '@/components/CartItemList.vue'
import InfoBlock from '@/components/InfoBlock.vue'
import axios from 'axios'
import { ref, computed, inject } from 'vue'

const props = defineProps({
  totalPrice: Number,
  vatPrice: Number,
})

const { cart, closeDrawer } = inject('cart')

const isCreating = ref(false)
const orderId = ref(null)

const createOrder = async () => {
  try {
    isCreating.value = true
    const { data } = await axios.post(`https://9a9662826ecf7816.mokky.dev/orders`, {
      items: cart.value,
      totalPrice: props.totalPrice.toFixed(2)
    })

    cart.value = []
    orderId.value = data.id
  } catch (err) {
    console.log(err)
  } finally {
    isCreating.value = false
  }
}

const cartIsEmpty = computed(() => cart.value.length === 0)
const buttonDisabled = computed(() => isCreating.value || cartIsEmpty.value)
</script>

<template>
  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
  <div class="bg-white w-full md:w-96 h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />

    <div v-if="!totalPrice || orderId" class="flex h-full items-center">
      <InfoBlock
        v-if="!totalPrice && !orderId"
        title="Сart is empty"
        description="Add at least one book to place an order"
        image-url="/package-icon.png" />

      <InfoBlock
        v-if="orderId"
        title="Order placed!"
        :description="`Your order #${orderId} will soon be transferred to the delivery service`"
        image-url="/order-success-icon.png" />
    </div>

    <div v-else class="h-full overflow-scroll pr-3">
      <CartItemList />

      <div class="flex flex-col gap-4 mt-7 mb-44">
        <div class="flex gap-2">
          <span>Total:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ totalPrice.toFixed(2) }}$</b>
        </div>

        <div class="flex gap-2">
          <span>Tax 5%:</span>
          <div class="flex-1 border-b border-dashed"></div>
          <b>{{ vatPrice }}$</b>
        </div>

        <button
          @click="createOrder"
          class="mt-4 bg-lime-500 w-full rounded-xl py-3 text-white hover:bg-lime-600 transition active:bg-lime-700 disabled:bg-slate-300 cursor-pointer"
          :disabled="buttonDisabled">
          Place an order
        </button>
      </div>

    </div>

  </div>
</template>