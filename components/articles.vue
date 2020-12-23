<template>
  <div class="col-span-2">
    <div class="space-y-4">
      <div class="flex items-center justify-between">
        <p class="text-xl font-semibold">Posts</p>
        <ul class="flex items-center text-gray-700">
          <li class="px-3 py-1 border-b-4 border-blue-600">Feed</li>
          <li class="px-3 py-1">Week</li>
          <li class="px-3 py-1">Month</li>
          <li class="px-3 py-1">Year</li>
          <li class="px-3 py-1">Infinity</li>
          <li class="px-3 py-1">Latest</li>
        </ul>
      </div>
      <article-loader v-if="$fetchState.pending" />
      <p v-else-if="$fetchState.error">An error occurred :(</p>
      <div v-else class="space-y-4">
        <post
          v-for="(post, p) in posts"
          :key="p"
          :post="post"
          :image="p === 0"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      posts: [],
    };
  },
  async fetch() {
    try {
      const { data } = await this.$axios.get("https://dev.to/api/articles");
      this.posts = data.map((item) => {
        return {
          title: item.title,
          image: item.cover_image ? item.cover_image : item.social_image,
          author: item.user.name,
          profile_image: item.user.profile_image,
          date: item.readable_publish_date,
          tags: item.tag_list,
          likes: item.public_reactions_count,
          comments: item.comments_count,
        };
      });
    } catch (err) {
      alert(err);
    }
  },
  fetchOnServer: false,
};
</script>