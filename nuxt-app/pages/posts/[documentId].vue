<!-- u18135600 Daniel Stevens -->
<template>
    <div class="Blog" v-if="post">
        <h1>{{ post.title }}</h1>
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p><strong>Category:</strong> {{ post.category }}</p>

        <div class="content" v-html="renderedContent"></div>
    </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import { marked } from "marked";

const route = useRoute();
const documentId = route.params.documentId;
const post = ref(null);
const renderedContent = ref('');

onMounted(async () => {
    const res = await fetch(`http://localhost:1337/api/posts?filters[documentId][$eq]=${documentId}`);
    const json = await res.json();
    post.value = json.data?.[0] || null;

    renderedContent.value = marked(post.value?.content || '')
})


</script>

<style scoped>
.Blog {
  max-width: 800px;
  margin: auto;
  padding: 2rem;
  background-color: #1b2f26;
  border: 2px solid #2d5f3b;
  border-radius: 8px;
  color: #e0e0e0;
}

h1 {
  color: #4eafc0;
}

strong{
    color: #398896;
}

.content {
  margin-top: 2rem;
  line-height: 1.6;
}

.content p {
  margin-bottom: 1rem;
}

.content h2 {
  color: #3e8a5e;
  margin-top: 1.5rem;
}
</style>