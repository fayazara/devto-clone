<template>
  <ul class="divide-y border-b">
    <li v-for="n in 5" :key="n" class="p-2">
      <div class="h-20 rounded bg-gray-200 animate-pulse"></div>
    </li>
  </ul>
</template>