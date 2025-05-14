<!-- u18135600 Daniel Stevens -->
<template>
    <div class="search">
        <h1>Search Blog Posts</h1>

        <input type="text" v-model="query" placeholder="Search by title or author...">

        <blogcard v-for="post in filteredPosts" :key="post.id":post="post"/>


    </div>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";

const posts = ref([]);
const query = ref('');

onMounted(async () => {
    const res = await fetch('http://localhost:1337/api/posts');
    const json = await res.json();
    posts.value = json.data || []
})

const filteredPosts = computed(() => {
  const q = query.value.toLowerCase()
  return posts.value.filter(post => {
    const title = post.title.toLowerCase()
    const author = post.author.toLowerCase()
    return title.includes(q) || author.includes(q)
  })
})

</script>

<style scoped>
.search {
  max-width: 800px;
  margin: auto;
  padding: 2rem;
  background-color: #1b2d2f;
  border: 2px solid #2d585f;
  border-radius: 8px;
  color: #e0e0e0;
}

h1 {
  color: #4eafc0;
}

input {
  padding: 0.5rem;
  width: 100%;
  border: 1px solid #2d585f;
  border-radius: 4px;
  background-color: #123335;
  color: #e0e0e0;
  margin-bottom: 2rem;
}
</style>
