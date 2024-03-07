<script setup>
import DrawerHead from './DrawerHead.vue'
import carditemlist from './CardLisItem.vue'
</script>
<template>

  <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-60"></div>
  <div class="w-96 bg-white h-full fixed right-0 top-0 z-20 p-8">
    <DrawerHead />
    <carditemlist/>
    <div class="flex flex-col gap-4 mb-6 my-7">
      <div class="flex gap-2 items-end">
        <span>Итого:</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>12900 p</b>
      </div>

      <div class="flex gap-2 items-end">
        <span>Налог 5%</span>
        <div class="flex-1 border-b border-dashed"></div>
        <b>900 p</b>
      </div>
      <button 
      disabled=""
      class="bg-slate-500 w-full disabled:bg-slate-300 rounded-xl py-3 hover:bg-line-600 active:bg-slate-700 cursor-pointer mt-4">
        Оформить заказ
      </button>
    </div>
  </div>
</template>