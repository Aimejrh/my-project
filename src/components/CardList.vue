<script setup>
import { inject } from 'vue';

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isFavorite: Boolean,
  isAddad: Boolean,
  onClickAddad: Function,
  onClickFavorite: Function,
})

</script>

<template>
  <div
    class="relative bg-white border-slate-100 rounded-3xl p-8 cursor-pointer transition-y-2 hover:translate-y-2 hover:shadow-xl">
    <img :src="!isFavorite ? './assets/favorite.svg' : '/assets/liked.svg'" alt="like 1"
      class="absolute top-8 left-8" @click="onClickFavorite">
    <img :src="imageUrl" alt="like 1">

    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between">
      <div class="flx float-col">
        <span class="text-slate-400">Цена:</span>
        <span>{{ price }}руб</span>
      </div>

      <img @click="onClickAddad" :src="!isAddad ? '/assets/plus.svg' : '/assets/btn-checked.svg'"
        alt="plus">
    </div>
  </div>
</template>