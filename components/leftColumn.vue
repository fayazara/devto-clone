<template>
  <div class="space-y-4">
    <div>
      <ul>
        <li v-for="(item, i) in items" :key="i">
          <div
            class="flex items-center space-x-4 px-1 py-2 rounded-md hover:bg-gray-200 text-gray-700"
          >
            <span class="text-2xl">{{ item.icon }}</span>
            <span>{{ item.title }}</span>
          </div>
        </li>
      </ul>
    </div>
    <div>
      <div class="flex items-center justify-between mb-4">
        <p class="text-xl font-sembold">My Tags</p>
        <button class="rounded hover:bg-gray-200 p-2">
          <img
            src="https://s.svgbox.net/hero-outline.svg?ic=cog&fill=grey-800"
            class="h-6 w-6"
          />
        </button>
      </div>
      <tags-loader v-if="$fetchState.pending" />
      <p v-else-if="$fetchState.error">An error occurred :(</p>
      <ul v-else class="h-64 overflow-y-scroll">
        <li
          v-for="(tag, t) in tags"
          :key="t"
          class="px-1 py-2 rounded-md hover:bg-gray-200 text-gray-700"
        >
          #{{ tag.name }}
        </li>
      </ul>
    </div>
    <div>
      <img
        class="rounded-md mb-4"
        src="https://res.cloudinary.com/practicaldev/image/fetch/s--pVCMYZWJ--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_350/https://scontent-lga3-1.cdninstagram.com/vp/7c898e2c9e9fa71f72dd5d422d444549/5DFE1BFA/t51.2885-15/fr/e15/s1080x1080/57390242_386431405416711_440644832181536446_n.jpg%3F_nc_ht%3Dscontent-lga3-1.cdninstagram.com"
        alt="Shop Banner"
      />
      <p class="text-center text-blue-700 font-semibold text-xl">
        Do you have your sticker pack yet?
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: "Home",
          icon: "🏡",
        },
        {
          title: "Reading List",
          icon: "📚",
        },
        {
          title: "Listings",
          icon: "📜",
        },
        {
          title: "Podcasts",
          icon: "🎙",
        },
        {
          title: "Tags",
          icon: "🔖",
        },
      ],
      tags: [],
    };
  },
  async fetch() {
    try {
      const { data } = await this.$axios.get("https://dev.to/api/tags");
      this.tags = data;
    } catch (err) {
      alert(err);
    }
  },
  fetchOnServer: false,
};
</script>