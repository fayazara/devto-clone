<template>
  <article class="rounded-md border bg-white">
    <img v-if="image" :src="post.image" />
    <div class="p-4">
      <div class="flex">
        <div class="flex-shrink-0">
          <img :src="post.profile_image" class="h-8 w-8 border rounded-full" />
        </div>
        <div class="ml-4 space-y-4 w-full">
          <dt>
            <p class="text-gray-600 font-semibold">{{ post.author }}</p>
            <p class="text-gray-500 text-sm">{{ post.date }}</p>
          </dt>
          <dt class="text-3xl font-bold text-gray-900">
            {{ post.title }}
          </dt>
          <ul class="flex space-x-2 text-sm">
            <li v-for="tag in post.tags" :key="tag">
              <span class="text-gray-400">#</span
              ><span class="text-gray-500">{{ tag }}</span>
            </li>
          </ul>
          <div class="flex items-center justify-between text-gray-600 text-sm">
            <div class="flex items-center space-x-2">
              <div class="flex items-center space-x-2">
                <img
                  src="https://s.svgbox.net/hero-outline.svg?ic=heart&fill=grey-600"
                  class="h-5 w-5"
                />
                <p>{{ post.likes }} Reactions</p>
              </div>
              <div class="flex items-center space-x-2">
                <img
                  src="https://s.svgbox.net/hero-outline.svg?ic=chat&fill=grey-600"
                  class="h-5 w-5"
                />
                <p>{{ post.comments }} Comments</p>
              </div>
            </div>
            <div class="flex items-center space-x-2">
              <p class="text-xs">2 min read</p>
              <button
                class="text-sm bg-gray-300 text-gray-700 rounded px-3 py-2"
              >
                Save
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

<script>
export default {
  props: ["post", "image"],
};
</script>