<script setup>
import { onMounted, ref, watch, reactive, provide } from 'vue';
import axios from 'axios'
import Header from './components/HeaderFaile.vue'
// import Card from './components/CardList.vue'
import CardList from './components/CardListEas.vue'
// import Drawer from './components/DrawerBlosk.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const onChaingeselect = (event) => {
  filters.sortBy = event.target.value
}

const onChaingSearchInput = (event) => [
  filters.searchQuery = event.target.value
]

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get(
      'https://f98439d04943312f.mokky.dev/favorites'
    );
    items.value = items.value.map(item => {
      const favorite = favorites.find(favorite => favorite.paramasId === item.id)

      if (!favorite) {
        return item;
      }
      return {
        ...item,
        isFavorite: false,
        favoriteId: favorite.id,
        isAdded: false
      }
    })
    console.log(items);
  } catch (error) {
    console.error(error);
  }
}

const addtoFavorites = async (item) => {
  try {
    if(item.isFavorite){

    }
    else if (!item.isFavorite) {
      const obj = {
        item_id: item.id
      }

      item.isFavorite = true

      const { data } = await axios.post('https://f98439d04943312f.mokky.dev/favorites', obj);

      item.favoriteId = data.id;
    } else {
      item.isFavorite = false;
      await axios.delete(`https://f98439d04943312f.mokky.dev/favorites/${item.favoriteId}`, obj);
      item.favoriteId = null;
    }
  } catch (error) {
    console.error();
  }
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }
    const { data } = await axios.get(
      'https://f98439d04943312f.mokky.dev/items',
      {
        params
      }
    );
    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      idAddad: false
    }))
  } catch (error) {
    console.error(error);
  }
}

onMounted(async () => {
  await fetchItems();
  await fetchFavorites();
});

watch(filters, fetchItems);

provide('addtoFavorites', addtoFavorites);
</script>

<template>
  <!-- <Drawer/> -->
  <div class="bg-white w-4/5 rounded-xl shadow-xl m-auto mt-14">
    <Header />
    <div class="p-10">
      <div class="flex justify-between items-center">
        <h2 class="text-3xl font-bold mb-8">Все кроссовки</h2>

        <div class="flex gap-4">
          <select @change="onChaingeselect" class="py-2 px-3 border rounded-md outline-none">
            <option value="name">По нозванию</option>
            <option value="price">По дешевле</option>
            <option value="-price">По дороже</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/assets/search.svg" alt="search">
            <input @input="onChaingSearchInput" type="text"
              class="border rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400" placeholder="Поиск... ">
          </div>
        </div>

      </div>
      <CardList :items="items" @addtoFavorites="addtoFavorites" />
    </div>
  </div>
</template>

<style scoped></style>
