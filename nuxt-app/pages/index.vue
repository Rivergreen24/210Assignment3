<!-- u18135600 Daniel Stevens -->
<template>
    <div class="home">
        <h1>Blog Homepage</h1>
        <label for="category">Filter by category:</label>
        <select name="category" id="category" v-model="selectedCategory">
            <option value="">All</option>
            <option v-for=" category in uniqueCategories" :key="category" :value="category">{{ category }}</option>
        </select>

        <blogcard v-for="post in filteredPosts" :key="post.id":post="post"/>
    </div>
</template>

<script setup>
import { ref,computed,onMounted } from "vue";
// import blogcard from '@/components/blogcard.vue'

const posts = ref([]);
const selectedCategory = ref('');

onMounted(async () => {
    const res = await fetch('http://localhost:1337/api/posts');
    const json = await res.json();
    posts.value = json.data || []
})

const uniqueCategories = computed(() => {
    return [...new Set(posts.value.map(p => p.category))];
})

const filteredPosts = computed(() => {
  if (!selectedCategory.value) return posts.value
  return posts.value.filter(p => p.category === selectedCategory.value)
})

</script>

<style>
.home {
  max-width: 800px;
  margin: auto;
  padding: 1rem;
}
</style>



























<!-- 
<template> testings
  <div class="container">
    <h1>Test Post (ID: 8)</h1>
    <div v-if="post">
      <h2>{{ post.title }}</h2>
      <p><strong>Author:</strong> {{ post.author }}</p>
      <p>{{ post.snippet }}</p>
    </div>
    <p v-else>Error fetching post: {{ errorMessage }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const post = ref(null)
const errorMessage = ref('')

onMounted(async () => {
  try {
    // Try single post endpoint
    const response = await fetch('http://localhost:1337/api/posts/8')
    if (!response.ok) {
      throw new Error('Failed to fetch post')
    }
    const data = await response.json()
    post.value = data.data || null
  } catch (error) {
    console.error('Single post error:', error)
    errorMessage.value = error.message
    // Fallback: Filter from list endpoint
    try {
      const listResponse = await fetch('http://localhost:1337/api/posts?filters[id][$eq]=8')
      if (!listResponse.ok) {
        throw new Error('Failed to fetch post list')
      }
      const listData = await listResponse.json()
      post.value = listData.data[0] || null
      if (!post.value) errorMessage.value = 'Post ID 8 not found in list'
    } catch (listError) {
      console.error('List fetch error:', listError)
      errorMessage.value = listError.message
    }
  }
})
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
}
</style> -->