<template>
  <div class="relative h-full flex items-center" @mouseenter="show = true" @mouseleave="show = false">
    <button
      class="rounded-full overflow-hidden focus:ring-2 focus:ring-offset-1 focus:ring-offset-white focus:ring-blue-800 focus:outline-none"
    >
      <img src="https://fayazz.co/fayaz.jpg" class="h-8 w-8" alt="Profile" />
    </button>
    <transition
      enter-active-class="transition-all ease-out duration-100"
      enter-class="transform opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition-all ease-in duration-75"
      leave-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <div
        v-if="show"
        class="bg-white w-56 rounded-md border-2 border-gray-900 absolute top-12 right-0 mt-2 super-shadow overflow-hidden origin-top-right"
      >
        <div class="p-2 border-b">
          <p>Fayaz Ahmed</p>
          <p class="text-sm text-gray-500">@fayaz</p>
        </div>
        <ul class="border-b p-2">
          <li class="py-2 pl-1 rounded hover:bg-gray-100">Dashboard</li>
          <li class="py-2 pl-1 rounded hover:bg-gray-100">Write a post</li>
          <li class="py-2 pl-1 rounded hover:bg-gray-100">Reading list</li>
          <li class="py-2 pl-1 rounded hover:bg-gray-100">Settings</li>
        </ul>
        <div class="p-2">
          <p class="py-2 pl-1">Sign Out</p>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
    };
  },
};
</script>

<style scoped>
.super-shadow {
  box-shadow: 4px 4px 0 #08090a;
}
</style>