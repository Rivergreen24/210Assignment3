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
  border: 1px solid #2d5f55;
  border-radius: 4px;
  margin-bottom: 1.5rem;
  background-color: #122835;
  transition: box-shadow 0.3s;
  color: #a1a1a1;
}

.post:hover {
  box-shadow: 0 0 8px rgba(45, 95, 59, 0.5);
}

h2 {
  margin-bottom: 0.5rem;
  color: #408e9c;
}

strong{
    color:#398896;
}

p {
  margin: 0.5rem 0;
}

a {
  display: inline-block;
  margin-top: 0.5rem;
  color: #9f5f24;
  font-weight: bold;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>