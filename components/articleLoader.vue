<template>
  <ul class="space-y-4">
    <li v-for="n in 3" :key="n">
      <div class="h-80 rounded-md bg-white overflow-hidden border">
        <div class="bg-gray-200 h-52 animate-pulse"></div>
        <div class="p-4">
          <div class="flex">
            <div class="flex-shrink-0">
              <div class="h-10 w-10 bg-gray-200 rounded-full animate-pulse" />
            </div>
            <div class="ml-4 space-y-4 w-full">
              <div class="h-10 rounded-full bg-gray-200 animate-pulse"></div>
              <ul class="flex items-center space-x-3 mt-4">
                <li
                  v-for="n in 3"
                  :key="n"
                  class="w-20 h-6 bg-gray-200 rounded-full animate-pulse"
                ></li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </li>
  </ul>
</template>