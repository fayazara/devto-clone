<template>
  <div class="w-auto ml-auto flex items-center space-x-4 h-full">
    <button
      class="px-4 py-2 rounded-md bg-blue-700 hover:bg-blue-800 text-white btn-focus"
    >
      Write a post
    </button>
    <button class="focus:outline-none rounded-full p-1 focus:bg-gray-200">
      <img
        src="https://s.svgbox.net/hero-outline.svg?ic=chat&fill=grey-700"
        class="h-6 w-6"
      />
    </button>
    <button class="focus:outline-none rounded-full p-1 focus:bg-gray-200">
      <img
        src="https://s.svgbox.net/hero-outline.svg?ic=bell&fill=grey-700"
        class="h-6 w-6"
      />
    </button>
    <profile />
  </div>
</template>

<style scoped>
.btn-focus {
  @apply focus:ring-2 focus:ring-offset-1 focus:ring-offset-white focus:ring-blue-800 focus:outline-none;
}
</style>