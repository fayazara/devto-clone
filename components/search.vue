<template>
  <div class="mx-4 w-96">
    <input
      type="text"
      placeholder="Search..."
      class="search-bar search-focus"
    />
  </div>
</template>

<style scoped>
.search-bar {
  @apply text-gray-600 placeholder-gray-600 rounded-md p-4 h-10 bg-gray-100 w-full border border-gray-400;
}
.search-focus {
  @apply focus:outline-none focus:ring-2 focus:ring-blue-600 focus:border-transparent;
}
</style>