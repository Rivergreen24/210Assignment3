<template>
  <div class="post">
    <h2>{{ post.title }}</h2>
    <p><strong>Author:</strong> {{ post.author }}</p>
    <p>{{ post.snippet }}</p>
    <NuxtLink :to="`/posts/${post.documentId}`">Read more</NuxtLink>
  </div>
</template>

<script setup>
defineProps({
  post: {
    type: Object,
    required: true
  }
})
</script>

<style scoped>
.post {
  padding: 1rem;
  border-bottom: 1px solid #ccc;
  margin-bottom: 1.5rem;
}
</style>