<script setup>

import { inject } from 'vue';

import CardList from './CardList.vue'
defineProps({
  items: Array,
})

const emit = defineEmits(['addtoFavorites']);

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <CardList
    v-for="item in items"
    :v-key="item.id"
    :id="item.id"
    :title="item.title" 
    :imageUrl='item.imageUrl' 
    :price="item.price"
    :isAddad="false" 
    :onClickFavorite=" () => emit('addtoFavorites',item)"
    :isFavorite="item.isFavorite"/>
  </div>
</template>