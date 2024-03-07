<template>
    <header class="flex justify-between border-b border-slate-200 px-8 py-8">
      <div>
        <img src="/assets/logo.png" alt="logo" class="w-10">
        <div>
          <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
          <p class="text-slate-400">магазин лучших кроссовок</p>
        </div>
      </div>
 
      <ul class="flex items-center gap-10 text-slate-500">
        <li class="flex items-center cursor-pointer gap-3 hover:text-black">
          <img src="/assets/cart.svg" alt="card">
          <span>1205 руб.</span>
        </li>
        <li class="flex items-center cursor-pointer gap-3 hover:text-black">
          <img src="/assets/heart.svg" alt="card">
          <span>закладки</span>
        </li>
        <li class="flex items-center cursor-pointer gap-3 hover:text-black">
          <img src="/assets/user.svg" alt="card">
          <span>профиль</span>
        </li>
      </ul>
    </header>
</template>