<template>
  <ul class="h-64 overflow-y-scroll space-y-2">
    <li
      v-for="n in 10"
      :key="n"
      class="h-10 rounded-md bg-gray-200 animate-pulse"
    ></li>
  </ul>
</template>