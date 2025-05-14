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

<style scoped>
.home {
  max-width: 800px;
  margin: auto;
  padding: 2rem;
  background-color: #1b2d2f;
  border: 2px solid #2d5c5f;
  border-radius: 8px;
  color: #a7a5a5;
}

h1 {
  color: #4eafc0;
}

label {
  display: block;
  margin-top: 1rem;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

select {
  padding: 0.5rem;
  width: 100%;
  border: 1px solid #2d5f57;
  border-radius: 4px;
  background-color: #122b35;
  color: #e0e0e0;
  margin-bottom: 2rem;
}




</style>

